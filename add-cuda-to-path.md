`vi` the instruction below into `.bashrc` so as not to keep enter them when restart the terminal
```
export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/targets/x86_64-linux/lib${LD_LIBRARY_PATH:+:${PATH:+:${LD_LIBRARY_PATH}}}
```