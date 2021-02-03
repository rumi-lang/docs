# Flow Control

Flow control in rumi is supported using the following statements.

## If

```
if (bool_expr) statement
else statement
```

Note that the else statement is optional:

```
if (bool_expr) statement
```

## While

```
while (bool_expr) statement
```

## Code Blocks

Code blocks are groups of statements packed together, and they could be used wherever a struct is required, for example, inside a while statement.

```
while (cond){
  // multiple statements
}
```
