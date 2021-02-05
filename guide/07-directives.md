# Compiler Directives

Compiler directives are ways for the program to modify the compilers behavior. Through them you can define new parsers, set compiler flags, or run any arbitrary functions. At the moment, we only have the @compile directive, defined the following way:

```
@compile
directive_name := (c: *Compiler) -> int{
  return 0;
}
```

## Compiler

The compiler struct has many methods, a complete list could be found in `tests/compiler.rum`, `tests/ast.rum` and `tests/parser.rum`.

## Return Value of Directives

The return value of a directive indicates whether the directive was successful (value of 0), wants to produce a warning (value of 1) or failed (any greater value). Note that on failure, the compiler will halt.

## Reader Macros

Reader macros are defined in directives to change the behavior of the system. To define a reader macro, you need a struct with `parse` and `genAST` methods defined, along with adding registering it as a parser to the program. 

```
// helper function
filetostring := (fname: string) -> string; // Load content of file, for an example definition look at `tests/argparse.rum`

// Reader macro
fromfile: struct{}
fromfile.parse := (c: *Compiler, s: *Source, pos: int) -> *ParseResult{
  idp := c.getIdParser();
  sp := c.getStringParser();

  id := idp.parse(c, s, pos);
  s := sp.parseAfter(id);

  // id would be null if no id was found.
  if(id){
     ids := id.getId(); // get its string value
     if(!streq(ids, "STRFROMFILE")){
       s = 0;
     }
  }
  return s;
}
fromfile.genAST := (c: *Compiler, token: *ParseResult) -> *C_AST{
  s_token :*CP_StringParser_ParseResult = token;

  s := c.createCString();
  s.setValue(filetostring(s_token.getValue()));
  return s;
}

// Directive to register it to the appropriate parser
@compile
test_compile := (c: *Compiler) -> int{

  c.set("removeMeta", true); // Add this line so that the reader macros doesn't end up in compiled code

  printf("This is compile time\n");

  c.registerParser("expression", "fromfile");

  return 0;
}
```

The previous code adds a reader macro that can read strings from file in compile time, i.e., parse the following program:

```
about_text := STRFROMFILE "about.txt";
```
