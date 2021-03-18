## gcc
`gcc` is GNU Compiler Collection, which can compile C/C++/Java. 

When you only got one .c file to compile, you can run shell command like below:
```
gcc file.c -o file
./file
```

## make
`make` is Unix utility that is designed to start execution of a `makefile`.

`makefile` is a special file, containing shell commands, that you create and name `makefile`.
```
make
./file
```

## cmake
`cmake` is a tool to generate `makefile` more conveniently, especially when it comes to the large project. 

You need to provide `CMakeLists.txt` to `cmake` to generate `makefile`