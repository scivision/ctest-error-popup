# CTest error popup

Demos CTest with a popup error dialog on Windows.
CTest uses libuv, which on Windows means that popup error dialogs are suppressed.
These dialogs would be useful to identify missing DLLs during CTest runs.
A sign of a missing DLL from a CTest test is `Exit code 0xc0000135`.

CTest error popups on Windows do not [work](https://cmake.org/cmake/help/latest/manual/ctest.1.html):

```sh
ctest --interactive-debug-mode 1
```

## Reproduce issue

On Windows:

```sh
cmake -Bbuild
cmake --build build

ctest --interactive-debug-mode 1 --test-dir build
```

the last command intentionally has a DLL that's in the build/lib/addone.dll and is not on PATH, and so error 0cx0000135 is issued.
We should also get an error popup window but we don't, unless manually running in command prompt `build/main.exe`.
