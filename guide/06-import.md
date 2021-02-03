# Import

Rumi allows the program to be written in multiple files through the import statement. Note that when importing another file, all of its content are read at that point and added to the program.

```
import name
```

Rumi initially searches the directory it was invoked in for the file name, and if it is unsuccessful, it will look at the `RUMI_PATH` environment variable which should be a colon separated list of paths, for example: `~/.local/share/rumi/:/usr/share/rumi`
