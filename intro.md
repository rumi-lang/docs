# Getting Started

To get started with rumi, have the following tools installed:

* LLVM11
* cmake
* a c compiler (gcc / clang)
* git

## Compilation

Clone the rumi code:

```
$ git clone https://github.com/MCSH/rumi
$ cd rumi
```

Prepare CMake:

```
$ cmake -H. -Bbuild
```

Compile it:

```
$ cmake --build build
```

Rumi is now available at `bin/rum`, you can add this to your path for your convenient.

## RUMI_PATH

Optionally, you can set the RUMI_PATH environment variable to allow access to a set of frequently used files. Since rumi lacks a standard library at the moment, we don't require this. But for your convenience you can set it to the `tests/` folder of the git directory, or you can create your own. We do suggest that you take the following files as is:

* compiler.rum
* parser.rum
* ast.rum

and take the content of this file, possibly modifying it for your needs `test_import`.

## Base example

Create a file named `getting_started.rum` and fill it with the following code:

```
printf := (f: string, a: ...any) -> unit; // printf declaration, you could instead import the test_import file

@compile
compile_time_directive := () -> int{
  printf("This is running in compile time!\n");
  return 0;
}

main := () -> int{
  printf("Hello Rumi!\n");
  return 0;
}
```

Now generate object files with:

```
$ rum getting_started.rum -o getting_started.o
$ gcc getting_started.o -o getting_started
```

Note that if you omit the `-o getting_started.o` in the first line, it will be written into `out.o`, and if you omit `-o geting_started` in the second line, it will be written into `a.out`.

To link with any C code you can include it in the arguments of the second file.
