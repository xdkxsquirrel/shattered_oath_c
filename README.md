# Shattered Oath

A C17 game using SDL3 and CMake.

## Debug in VS Code on Windows

The workspace uses the MSYS2 MinGW64 toolchain installed at
`C:/msys64/mingw64/bin` and the Microsoft **C/C++** extension. **CMake Tools**
is also recommended. If MSYS2 is installed elsewhere, update the paths in
`.vscode/launch.json`, `.vscode/tasks.json`, and `.vscode/settings.json`.

If GDB is missing, install it from an MSYS2 terminal:

```sh
pacman -S --needed mingw-w64-x86_64-gdb
```

1. Open this project folder in VS Code.
2. Press **F5** and select **Debug Shattered Oath** if prompted. The task
   configures and builds `build/shattered_oath.exe` in Debug mode before launch.
   The first build downloads and compiles SDL3, so it needs internet access.
3. Execution pauses automatically on the first statement in `SDL_AppInit`
   in `main.c`, before the game window opens.
4. Use **F10** to step over, **F11** to step into, **Shift+F11** to step out,
   and **F5** to continue. Inspect values in **Variables** and **Watch**,
   or hover over a variable while paused.
5. Click beside a line number or press **F9** to toggle a breakpoint.
   `SDL_AppIterate` handles each frame; `SDL_AppEvent` handles input and
   window events. A breakpoint in `SDL_AppIterate` will pause every frame.
6. Press **Shift+F5** to stop debugging.

**Ctrl+Shift+B** builds the Debug executable without launching it. The existing
`build.sh` and `run.sh` scripts use the same build directory.

The debugger uses a temporary breakpoint in `SDL_AppInit` because SDL supplies
the program's `main` function. Remove that breakpoint entry from `setupCommands`
in `.vscode/launch.json` if you prefer to pause only at your own breakpoints.

See the [VS Code MinGW debugging guide](https://code.visualstudio.com/docs/cpp/config-mingw)
for the compiler and debugger setup.
