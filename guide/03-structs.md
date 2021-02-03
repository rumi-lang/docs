# Structs

Structs in rumi are defined in top level with the following syntax:

```
struct_name: struct{
  // fields, for example:
  int id;
}
```

You have access to their size by calling `sizeof struct_name` and can access their members by adding a `.` after their variable name.

```
a: struct_name;
a.id = 10;
printf("a.id = %d\n", a.id);
```

## Methods

Methods are functions defined on a struct, and they have access to a member of their type through the `self` variable. for example:

```
struct_name.print := () -> unit {
  printf("<struct_name :id = %d>\n", self.id);
  return ;
}

main := () -> int{
  a: struct_name;
  a.print();
  return 0;
}
```

## Pointers to structs

Pointers to structs are defined like regular pointers, however, you can easily access their members and methods through shortcuts, e.x.:

```
a: *struct_name;
a.id = 10; // works, even though a is a pointer
a.print();
```

## Constructors

A constructor is defined this way:

```
new struct_name := () -> unit{
  // You have access to self here
  return;
}
```

Note that at the moment constructors don't get any arguments and are called only for on stack initialization. This behavior is subject to change.

## Binary Operators

A binary operator could be defined on any struct and any type, but left hand side must always be a struct. These four types are possible in general:

```
struct_name op type := (lhs: struct_name, rhs: type) -> return_type { /*...*/ }
struct_name op type := (lhs: *struct_name, rhs: type) -> return_type { /*...*/ }
struct_name op type := (lhs: *struct_name, rhs: *type) -> return_type { /*...*/ }
struct_name op type := (lhs: struct_name, rhs: *type) -> return_type { /*...*/ }
```

The compiler handles the pointers, so you don't need to worry about them. The possible ops are:

```
* +
* -
* *
* /
* %
* ==
* <
* <=
* >
* >=
```
