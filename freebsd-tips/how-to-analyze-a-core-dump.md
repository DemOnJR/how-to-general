# How to analyze a core dump

We usually use the GDB (gnu debugger) to achieve this.

We go to the relative path in which the executable and the core dump has been generated and start gdb.

After that, we send some specific instructions.

```sh
# we go to the specific path (this is just an example of path)
cd /usr/home/main/srv1/chan/ch1/core1/
# we run gdb (or gdb811 if updated; numbers may change)
gdb
# we set the gnutarget flag (no need if it's a 64bit binary)
set gnutarget i386-marcel-freebsd
# we specify the relative executable from which the core has been generated
# (if you recompile the executable and replace it, you will see junk)
file srv1-ch1-core1
# specify the core dump file
core game.core
# show the stack call
bt
```

In case it says "dwarf error", you have to install the latest gdb and [run it as gdbXXX instead of gdb](https://gyazo.com/8927fe0cd80f048662ec9914916dac6f), for example:

```sh
# search the pkg
pkg search gdb
>gdb-8.1_1                      GNU GDB of newer version than comes with the system
# install it
pkg install gdb-8
# now search how the binary name is called
gdb[PRESSTAB]
>gdb        gdbm_dump  gdbmtool   gdbtui
>gdb801     gdbm_load  gdbserver  gdbtui801
# now to run it, you must call it gdb8 instead of gdb
gdb801
```

The instruction `bt full` returns the full backtrace, instead of doing just `bt`.

On updated fbsd versions, the gnutarget may be `i386-portbld-freebsd10.1` instead of `i386-marcel-freebsd`.

Important: the executable must be the original one; recompiled executables will give mismatched results.
