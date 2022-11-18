## Include CUDA to your path
`vi` the instruction below into `.bashrc` so as not to keep enter them when restart the terminal
```
export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/targets/x86_64-linux/lib${LD_LIBRARY_PATH:+:${PATH:+:${LD_LIBRARY_PATH}}}
```

## NVIDIA System Management Interface
```
nvidia-smi 
```
|    Option    |                                             Function                                            |
|:------------:|:-----------------------------------------------------------------------------------------------:|
| -l [seconds] | Continuously report query data at the specified interval, rather than the default of just once. |
| -i [gpuid]   | Display data for a single specified GPU or Unit.                                                |
| -L:          | List each of the NVIDIA GPUs in the system, along with their UUIDs.                             |
| -q           | Display GPU or Unit info.                                                                       |
| -i           | Display data for a single specified GPU or Unit.                                                |
| -f [file]    | Redirect query output to the specified file in place of the default stdout.                     |

## NVIDIA's CUDA Compiler 
```
nvcc --version
```