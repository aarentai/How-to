## Check info of a process
|        Terminal 1        |               Terminal 2               |
|:------------------------:|:--------------------------------------:|
| `make qemu-nox-gdb`      |                                        |
|                          | `gdb`                                  |
| Run a process, e.g. `ls` |                                        |
|                          | `p *myproc()` or `p *myproc()->parent` |

## Check info of a register
|      Terminal 1     | Terminal 2 |
|:-------------------:|:----------:|
| `make qemu-nox-gdb` |            |
|                     | `gdb`      |
|                     | `b _start` |
|                     | `c`        |
|                     | `info reg` |
|                     | `stepi`    |
|                     | `info reg` |