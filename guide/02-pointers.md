# Pointers

Pointers in rumi are defined by adding a `*` before a type, for example `*u8` or `*Compiler`. When a concept has a pointer to a type, it could be dereferenced via `*id`, and a pointer to a concept could be acquired by `&id`. Pointers could potentially be null.

## Operations

Pointers have the following operations defined on them:

* `!ptr` ->  `bool`: returns true if the pointer is null (has value 0)
* `ptr` + `int` -> `ptr`: moves that amount forward or backward in memory, with steps of the underlying size.

## Allocation

Pointers are allocated on the stack, however, their value could live anywhere. Rumi doesn't provide a standard way of allocation (yet), but you can use `malloc` to assign on heap. Beware of stack assignment and pointers, they are not reliable if the function exits.

## Value accessing

Values of a pointer could be accessed by adding a `*` before their name, e.x.,:

```
p: *int;
p = malloc(sizeof int);
*p = 10;
printf("p points to a place in memory that has %d\n", *p);
```

## Address accessing

Pointers can capture address of an alloca using `&`, this address is usually on the heap.

```
a = 10;
p: *int = &a;
printf("a = *p = %d", *p);
```

## Indexing

A pointer of type `a` is similar to an array of type `a`, you can access their internal by indexing them with `[]`, for example:

```
p : *int = malloc(sizeof int * 10);
p[0] = 10;

printf("p[1] == *(p + 1) == %d\n", p[0]);
```
