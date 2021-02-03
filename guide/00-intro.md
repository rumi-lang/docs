# Introduction

Rumi is a WIP programming language, developed by Sajjad Heydari <mcshemail@gmail.com>, aiming to make programming joyful by allowing a compiler API available during compile time to allow for custom code generation, reader macros, etc. Rumi can be easily linked with C code (and therefore other programming languages), and relies on LLVM to generate object codes. Rumi uses symbols wherever appropriate.

Rumi source code is created out of Concepts, they could be functions, types, variable or data. To define a concept, we use this syntax:

```
concept_id : concept_type = concept_value
```

only one of the `concept_type` and `concept_value` is necessary, where appropriate the compiler can resolve the type from value. To use a concept, you use its `concept_id`. Rumi's source code by default is constructed out of different parsers:

* Top Parser: These parse parts of the code that live in the outer most section of the source code. They include things like function, method, struct and interface definitions, along with import statement and compiler directives.
* Type Parser: These parse parts of the code that describe a type, they could be primitives, pointers or named types.
* Statement Parser: These parse parts of the code that make a statement, including branching operators such as if and while, variable definition, function calls and return statements.
* Expression Parser: Expressions are things that could be either stored in variables or passed into functions. They include casts, variable usage, pointer reference and different types of operations.
* Value Parser: These are a more general category for values, they consist of all of expressions, as well as things that can go directly in the define syntax. Any expression followed by a semicolon is considered a value, however, not all values require semicolons at the end, for example the function definition.

## Symbols

The following symbols have special meaning in Rumi:

* `->`: conversion, used in casting and function definition, `A->B` means A is being converted to B.
* `:` type, used in definitions, `A:B` means A has the type B.
* `=` assignment, used in assignment, definition and comparison, `A=B` means store value of B in A, and `A==B` means check whether A is equal to B.
* `()` encapsulation, used in function definition and expressions, values inside parenthesis are capsuled together
* `{}` context, used in function/if/while bodies, also acceptable wherever there is a need for a statement.


## Functions

Functions are pieces of code that convert their arguments to their return type, possibly producing side effects in the process. 

Functions are added to a program either through a declaration or a definition. Declaration only adds the signature of a function and is used to either let the compiler know about a function that is going to be used before their definition, or if the function is going to be linked separately. Definition on the other hand, actually contains the body of the function.

```
// Declaration:
exit_with_error := (e: string) -> unit;

// Definition:
exit_with_error := (e: string) -> unit {
  printf("%s\n", e);
  exit(1);
  return ; // Returns are required for all functions at the moment, this will be fixed.
}
```

Note that if the return type is unit, the definition could omit the `->unit` part.

The entry point of any program is the main function, that could be defined with any of the following signatures:

* `(argc: int, argv: *string) -> int`, the first argument provides the number of arguments, the second one their array in form of a pointer, and the return type is the exit status of the program, with 0 being normal.
* `(argc: int, argv: *string, env: *string) -> int`, similar to the previous one, but the third argument captures the environment. NOTE: Although this style is available in UNIX, it is not in the POSIX standards, so to write portable code you should avoid it and rely on getenv to access environment variables.
* `() -> int`, the arguments aren't passed down to the program
* `() -> unit`, the exit status is always zero, unless they exit with `exit(status: int)->unit`. NOTE: you can remove the `->unit` part if you are writing the function definition.
