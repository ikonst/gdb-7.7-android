GDB 7.7 for Android debugging
=============================

Win32 binaries of gdb-7.7 which I've built to work around [Android issue 78239: gdb 7.6 resolves symbols very slowly in C++ stack frames](https://code.google.com/p/android/issues/detail?id=78239).

Unlike Google's build, my build lacks Python support but has libiconv (i.e. set host-charset, target-charset and target-wide-charset) support.

To install:

1. Copy `libiconv-2.dll` to `$NDK\prebuilt\windows-x86_64\bin\libiconv-2.dll`
2. Copy `gdb.exe` to `$NDK\toolchains\arm-linux-androideabi-4.8\prebuilt\windows-x86_64\bin\arm-linux-androideabi-gdb-orig.exe`
3. Copy `gdb.exe` to `$NDK\toolchains\arm-linux-androideabi-4.9\prebuilt\windows-x86_64\bin\arm-linux-androideabi-gdb-orig.exe`
4. Copy `gdbserver` to `$NDK\prebuilt\android-arm\gdbserver\gdbserver`

To build from sources:

1. Install MinGW32 packages `mingw32-base`, `mingw32-gcc-g++` (required by expat), `msys-bison` (required by gdb) and `libiconv-dev` (used by gdb)
2. `mount c:/mingw /mingw`
3. Build expat:
   1. Download expat (in my case, it was 2.1.0)
   2. `tar xzfv expat-2.1.0.tar.gz && cd expat-2.1.0 && ./configure --prefix=/mingw && make && make install`
4. Build gdb:
   1. Clone Android gdb from https://android.googlesource.com/toolchain/gdb.git
   2. `cd gdb/gdb-7.7 && ./configure --prefix=/mingw --target=arm-linux-androideabi && make`
