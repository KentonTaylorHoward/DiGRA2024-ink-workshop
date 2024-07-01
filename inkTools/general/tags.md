# Tags

Each line in ink can carry additional data as part of a concept named *tags*. These are created using the hash, `#`, symbol followed by a name for the tag.

```ink
This is a line. #This is a tag.
```

Tags are removed from output. They are metadata used with meaning outside of the content of the story itself.

## Multiple Tags

While tags are loaded on a per-line basis, there is no limit to the number of tags per line. Each new tag need only be preceded by a hash.

```ink
This is a line. #This is a tag. #This is another tag.
```

## Tags and Glue

The use of glue in ink, combination of less-than and greater-than symbols together, "glues" lines together. Any tags used as part of lines
containing glue are considered part of the same "line" internally by ink.

```ink
This <> #This is one tag
one single <> #This is a second tag
line internally. #This is a third tag
```

In the previous example, because of the use of glue in ink, three tags are part of a single line internally in ink.

## Review

Tags are added on a per-line basis using a hash followed by text.

Multiple tags can be used on the same line.

Because tags are used on a per-line basis, they are affected by glue. Tags will be gathered until the "line" ends.
