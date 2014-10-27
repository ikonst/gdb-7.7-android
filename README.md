GDB 7.7 for Android debugging
=============================

Win32 binaries of gdb-7.7 which I've built to work around [Android issue 78239: gdb 7.6 resolves symbols very slowly in C++ stack frames](https://code.google.com/p/android/issues/detail?id=78239).

Sorry, unlike Google's build, my build lacks Python support..

To install:

2. Copy `gdb.exe` into `$NDK\toolchains\arm-linux-androideabi-4.8\prebuilt\windows-x86_64\bin\arm-linux-androideabi-gdb.exe`
3. Copy `gdbserver` into `$NDK\prebuilt\android-arm\gdbserver\gdbserver`

If you're using gcc 4.9, use `arm-linux-androideabi-4.9` instead.
Afterwards you may delete `arm-linux-androideabi-gdb-orig.exe` since it's no longer used.

To build:

1. Install MinGW32 packages `mingw32-base`, `mingw32-gcc-g++` (expat requires) and `msys-bison` (gdb requires)
2. `mount c:/mingw /mingw`
3. Build expat:
   1. `tar xzfv expat-2.1.0.tar.gz && cd expat-2.1.0 && ./configure --prefix=/mingw && make && make install`
4. Build gdb:
   1. Clone Android gdb from https://android.googlesource.com/toolchain/gdb.git
   2. `cd gdb/gdb-7.7 && ./configure --prefix=/mingw --target=arm-linux-androideabi && make`
