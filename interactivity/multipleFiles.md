# Multiple Files

For complex projects, not only can stories be broken into knots and stitches, it is also possible to use multiple files. In ink, the keyword `INCLUDE` can be used with the relative path to a file containing ink code. Any knots within other files will then be considered part of the same story.

When using multiple files, it is strongly recommended to use the ".ink" filetype and to keep all files within the same directory.

**Main.ink**

```ink
INCLUDE Variables.ink

The current health is {health}.
```

**Variables.ink**

```ink
VAR health = 10
```

## Review

The INCLUDE keyword can be used in ink to "include" the contents of another file in the current story. This is a common way to better
organize large and complex stories into separate files with their own knots and stitches.
