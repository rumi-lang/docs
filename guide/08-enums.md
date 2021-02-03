# Enums

Enums are currently implemented using integers in the following way:

```
enum_name: enum{
  // values
  v1,
  v2,
  // optionally values could have integers assigned to them
  v3 = 5,
}
```

You can use them in the following way:

```
a: enum_name;
a = v1;
a = v3;
```
