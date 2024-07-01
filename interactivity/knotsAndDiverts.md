# Knots and Diverts

Most interactive stories are nonlinear. Rather than a straightforward progress from one section to another, it is possible to move between
them in more complicated ways.

In ink, a story can be divided into sections named *knots*.

## Dividing up a story

We can create a knot in ink using two equal signs and a name for the section.

```ink
== chapter1
```

**Note**: There are special rules for the names of knots. They can contain letters, numbers, and the underscore, but cannot use spaces or
other special symbols. (These match the same rules of naming variables.)

## Moving through a story

We move from one section of a story to another using a *divert*. This "points" to the name of the knot using a minus and greater-than symbol combination.

```ink
-> chapter1

== chapter1
In the beginning, the story started.
```

The flow of a story follows the use of diverts and knots. It is "diverted" across different sections based on what is encountered during
a session.

A story without an ending is an issue and will result in an error.

To fix this, we need to use a special knot in every story.

## Making an ending

In a nonlinear story, knowing where a story ends becomes difficult. To help with this issue, ink defines a special knot available to every
story: `END`. Every story using knots and diverts must define an end.

```ink
-> chapter1

== chapter1
In the beginning, the story started.
-> END
```

Without the use of the END knot, an ink story will not run. It must have a defined flow with an END.

## Knots and stitches

We can divide up a section of a story into subsections. In ink, a section is a knot and a subsection is a *stitch*.

The naming convention of stitches follows the same for knots: letters, numbers, and the underscore. No spaces or special symbols can be used.

A stitch is created using a single equal sign within a knot.

```ink
-> TableOfContents

== TableOfContents

= Chapter1
This is chapter 1.
-> END

= Chapter2
This is chapter 2.
-> END

= Chapter3
This is chapter 3.
-> END
```

The first stitch in a knot is considered the default when the flow of a story is diverted to the section. When the story moves to this location, the first stitch’s content will always be accessed.

Accessing a stitch within a knot follows a *dot notation*. The name of the knot is first and the stitch second with a period, ., between them. In the previous example, the second chapter could be accessed by using the divert target of *TableOfContents.Chapter2*.

```ink
// Divert directly to Chapter 2
-> TableOfContents.Chapter2

== TableOfContents

= Chapter1
This is chapter 1.
-> END

= Chapter2
This is chapter 2.
-> END

= Chapter3
This is chapter 3.
-> END
```

In the previous example, the flow of the story immediately moves to the stitch *Chapter2* within the knot *TableOfContents*. Because the
*TableOfContents* knot diverts to the END knot, the story ends.

## Review

In ink, we can divide up a story into sections named knots.

Knots can then be subdivided into stitches.

To change the flow of a story, we use a divert.

When using a divert, we can change the flow of a story to a knot or a stitch. When diverting to a stitch, the naming convention is to
reference the knot and then name of the stitch using a period between them. By default, diverting the flow of a story to a knot containing at least one stitch will also include the first stitch encountered as well.
