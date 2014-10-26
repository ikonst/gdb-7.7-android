Win32 build of GDB 7.7 for Android ARM debugging
================================================

gdb 7.6 (shipped with Android NDK r10c) suffers from [this bug](https://sourceware.org/bugzilla/show_bug.cgi?id=15519) (fixed in gdb 7.7) which makes symbol resolving unbearably slow within C++ code (when the stack frame was in a C++ class).

The symptom:

````(gdb) print global_symbol````

takes >30 seconds (when called within a C++ frame),

````(gdb) print this->global_symbol````

also takes >30 seconds, but

````(gdb) print ::global_symbol````

works returns right away.

This is [Android's gdb-7.7](https://android.googlesource.com/toolchain/gdb.git/+/master/gdb-7.7/) built with MinGW.

To deploy:

* move gdb.exe to $NDK\toolchains\arm-linux-androideabi-4.8\prebuilt\windows-x86_64\bin\arm-linux-androideabi-gdb.exe
* move gdbserver to $NDK\prebuilt\android-arm\gdbserver
