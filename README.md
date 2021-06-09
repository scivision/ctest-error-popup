# CTest error popup

Demos CTest with a popup error dialog on Windows.
Currently there seems to be a bug with CTest on Windows such that popup error dialogs are suppressed.
These dialogs can be useful to identify missing DLLs during CTest runs.
A sign of a missing DLL from a CTest test is `Exit code 0xc0000135`.

It's expected that CTest error popups on Windows
[should work](https://cmake.org/cmake/help/latest/manual/ctest.1.html) with:

```sh
ctest --interactive-debug-mode 1
```

However this is not the case, at least with CMake 3.13.5 and 3.20.3 (and probably many other versions) on Windows 10.
I tried this with GCC 10.3 from MSYS2 and VS 2019 16.10.

## Reproduce issue

On Windows:

```sh
cmake -Bbuild
cmake --build build

ctest --interactive-debug-mode 1 --test-dir build
```

the last command intentionally has a DLL that's in the build/lib/addone.dll and is not on PATH, and so error 0cx0000135 is issued.
We should also get an error popup window but we don't, unless manually running in command prompt `build/main.exe`.
