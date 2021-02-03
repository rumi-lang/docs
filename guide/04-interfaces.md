# Interfaces

Interfaces in rumi are defined in top levels with the following syntax:

```
interface_name: interface{
  // methods, for example:
  print := () -> unit;
};
```

You can assign a struct to the interface only if the struct implements all of its methods.
