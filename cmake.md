### Configure

Linux:

```bash
cmake -B build/Debug -D CMAKE_BUILD_TYPE=Debug -D CMAKE_EXPORT_COMPILE_COMMANDS=ON -G Ninja
ln -sf Debug/compile_commands.json build/
```

Windows:

```cmd
cmake -B build/Debug -D CMAKE_BUILD_TYPE=Debug -D CMAKE_EXPORT_COMPILE_COMMANDS=ON -G Ninja
set "MSYS=winsymlinks:nativestrict" && ln -sf Debug/compile_commands.json build/
```

#### Notes

* Set additional env vars with the `-D` flag.
* The ninja generator is nice because it supports both gcc/clang and msvc builds.
    * To force cmake to use clang proper (not clang-cl) and also target the Microsoft C library, make sure your shell session is set up with visual studio's development vars (`vcvars64.bat`) and use the following extra cmake options in the configure command: `-D CMAKE_C_COMPILER="C:\Program Files\LLVM\bin\clang.exe" -D CMAKE_CXX_COMPILER="C:\Program Files\LLVM\bin\clang++.exe" -D CMAKE_C_COMPILER_TARGET=x86_64-pc-windows-msvc -D CMAKE_CXX_COMPILER_TARGET=x86_64-pc-windows-msvc`.
    * For projects targeting the Microsoft C library, you can use [raddebugger](https://github.com/EpicGamesExt/raddebugger) for debugging instead of having to fire up visual studio.
* To cross compile a windows app on linux, add: `-D CMAKE_SYSTEM_NAME=Windows -D CMAKE_C_COMPILER=x86_64-w64-mingw32ucrt-gcc -D CMAKE_CXX_COMPILER=x86_64-w64-mingw32ucrt-g++ -D CMAKE_FIND_ROOT_PATH=/usr/x86_64-w64-mingw32ucrt/sys-root/mingw -D CMAKE_FIND_ROOT_PATH_MODE_PROGRAM=NEVER -D CMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY -D CMAKE_FIND_ROOT_PATH_MODE_INCLUDE=ONLY`
* `s/Debug/Release/g` for release build.
* The `set` command above is needed for windows because by default the mingw version of `ln` will copy files instead of symlinking. Could also just use `mklink` but mklink is cringe (not unlike most native windows utilities) because it doesn't have the equivalent of ln's `-f` flag.

### Build

Linux:

```bash
cmake --build build/Debug -j $(nproc)
```

Windows:

```cmd
cmake --build build/Debug -j %number_of_processors%
```

#### Notes

* `s/Debug/Release/g` for release build.
