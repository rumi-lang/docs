Rumi's language definition.

This document is a WIP.

# Concepts

`Concepts` are the core of `rumi`. A concept is any piece of code that either contains data or procedure or both. That includes:

* functions and methods
* variables and constants
* types including primitives, enums, structs and interfaces
* compiler directives

All concepts have an identifier (or `id`), as well as types. To define any new concept, we should:

``` rumi
id : type = value;
id : type;
id := value;
```

If the type can be infered from the value it can be ommited. In a similiar fashion, if there are no values for that type, or if the value is going to be assigned later (in case of variables), it could be ommited.


# Common Notations

The main notations (symbols) in rumi are:

* `:` the type
* `*` pointers
* `->` conversion (as in casting or functions)
* `=` equality (`=` assignment, `==` comparison)
* `@` compiler action, i.e., compiler directives

The syntax of rumi is developed with these notations in mind.

# Primitive Types

Rumi includes the following primitive types:

* `void` a non-existance of instance. i.e., it's impossible to have a variable of this type (even nil isn't a member here), and it should be only used in return types.
* `any` a default arch-dependent value, usually 32 or 64. This is often used with pointers to emulate `void *` in c family.
* `int` a arch-dependent signed integer, usually 32 or 64.
* `u8`, `u16`, `u32`, `u64` unsigned integer of various sizes.
* `s8`, `s16`, `s32`, `s64` signed integer of various sizes.
* `f32`, `f64`, floating point of various sizes (float, double in c family)
* pointers
* `string`, pointers to `u8`, WIP
* `arrays`, pointers to specific type OR fixed size arrays, WIP
* function pointers

# enum

An `enum` is defined as:

``` rumi
enm : enum {
  v1, v2, // note the trailing comma
}
```

optionally default values could be provided:

``` rumi
enm: enum {
  v1 = 10, ve = 12,
}
```

And it is used like:

```rumi
a : enm = enm.v1;

if(a == enm.v2){
   // whatever
}
```

# structs and interfaces

A `struct` is defined as:

``` rumi
id : struct {
  field1 : type;
  field2 : type;
}
```

and represent data in memory. `struct`s can have methods associated with them, where a variable, `self` will be a pointer to them:

``` rumi
id.method := () -> {}
```

`interface`s are defined as:

``` rumi
id: interface {
  mtd1 := () -> void;
  mtd2 := (a: int, b: int) -> void;
}
```

A struct implements an interface if:

* it has all of its methods and is casted (directly or indirectly) to that interface in code
* or, it has all of its methods and the compiler is instructed to implement the cast codes (WIP)

interfaces can define other methods as well, simliar to structs. The difference is that when a method is mentioned inside the interface, it should be implemented by the struct, but when it is defined outside, it will be available to structs that have implemented it (WIP).

# functions

Functions' concept types are ommited in the current version, since their value must include their type anyways. One can define a function in place or just define the signature, so that the body could be implemented in another location of the code.

``` rumi
fn := (inp1: type1, inp2: type2, inp3: ...type3) -> out_type; // function signature with vardiac input

// function in place definition
fn := () -> void {
  return ;
}
```

Vardiac operations are understood for the signature, but are WIP for definition.

# flow control

Currently rumi supports `if/else` and `while` operations. 

``` rumi
if(a)
  something
else
  something else


while(b)
  loop_code

```

The else statement is optional. If there are more than one line of code required in each segment, one can supply `{}` around the code block.

# Misc

Currently rumi has support for:

* `return` which returns the function, optionally an expression could follow
* `sizeof` which returns the size of the type in front of it, e.x., `sizeof *any`

# Operations

* `+-*/%`
* `== >= <= > < !=`
* `!`

# Compiler Directives

A compiler directive is in the form `@id` and could be followed by anything, depending on the directive. Currently the following are designed:

* `@compile` followed by a function definition, runs the function in compile time. The function *MUST* have a return type of integer that is used to assess if the compile should continue (return 0), issue a warning (return 1) or fail (any other value)
* `@define` followed by a function definition, defines a new compile directive. 
