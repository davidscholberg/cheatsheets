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
