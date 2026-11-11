cmake_minimum_required(VERSION 3.28)
project(ShatteredOath VERSION 0.1.0 LANGUAGES C)

set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)  # writes compile_commands.json for editor tooling

# --- Dependencies -------------------------------------------------------------
include(FetchContent)

# Build SDL as a static library, so the game is a single .exe with no SDL3.dll.
set(SDL_SHARED OFF)
set(SDL_STATIC ON)
set(SDL_TEST_LIBRARY OFF)

FetchContent_Declare(
    SDL3
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG        release-3.4.18  # pinned so every build uses the same SDL
    GIT_SHALLOW    TRUE            # fetch only that commit, not the full history
    SYSTEM                         # treat SDL's headers as system headers (no warnings)
    EXCLUDE_FROM_ALL               # only build the parts of SDL we link against
)
FetchContent_MakeAvailable(SDL3)

# --- Game: Shattered Oath itself -----------------------------------------------
add_executable(shattered_oath
    main.c
)
target_link_libraries(shattered_oath PRIVATE SDL3::SDL3)

if (MSVC)
    target_compile_options(shattered_oath PRIVATE /W4)
else()
    target_compile_options(shattered_oath PRIVATE -Wall -Wextra -Wpedantic)
endif()
