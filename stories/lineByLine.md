# Line By Line

We write a story in ink by writing a story. The output of a story, what is generated for a reader, will appear nearly the same as it does when we write it with a few important exceptions. Throughout this workshop, we will learn these exceptions and how they affect what is presented to a reader.

We begin with two important and interconnected terms: flow and lines.

## Flowing downward

When writing a story, one sentence appears after another. We may edit out of sequence and fix any issues, but what is produced with a work
will be multiple sentences in a specific order to create meaning. When a reader encounters the written story, they would read it from top to bottom, moving from one sentence to another. This is the same with ink. It *flows* from top to bottom.

**The flow of a story moves from one line to the next.**

For example, a simple ink story might only contain three lines from the play *Wicked* (book by Stephen Schwartz):

```ink
Don't wish.
Don't start.
Wishing only wounds the heart.
```

The flow of the story would move across the lines in the previous example as they are encountered by a reader. This may seem very simple,
but understanding the flow of a story is an important aspect of creating with ink. It moves *line by line*.

When writing a story, we may often want to add notes for ourselves or our collaborators. In ink, this is known as a *comment*, which looks
like this:

```ink
// I am a comment!
I am text!
```

## Reminders and notes

Each comment is its own line. We can use them to break up larger content into smaller parts where we leave notes for ourselves and others to better understand the content. When the content is processed, comments are removed from potential output.

```ink
// Do we really want to quote song lyrics here? Will that be a copyright issue?
Well, people, I've been here before.
// What if we re-worded this slightly?
I've walked this floor and seen this room.
```

In the previous example, the first and third lines are comments. They will not be shown to a reader.

In the screenshot above, the comments can be seen in the code on the right, and what will be shown to the reader appears on the left - note
that the comments do not appear there!

Like many languages, there are also exceptions to rules. By default, each line in ink will be separate. This is true of most content and all comments. However, there is a way to have one output line merged into the next. In ink, this is known as using *glue*.

## Gluing lines

Each line is separate. However, it is possible to merge lines using *glue*: a special combination of less-than and greater-than symbols
together. When processed, whatever follows the glue will be "glued" with whatever was before it.

```ink
All of this <>
is one line <>
glued <>
together.
```

In the previous example, the four different lines will appear as one in the output of the story.

Comments are removed from output to readers. This means glue will combine any lines across comments as well.

```ink
All of this <>
// This comment interrupts but will not be shown.
is one line <>
// This comment also interrupts but will not be shown.
glued <>
together.
```

Glue is a useful tool in ink for when we want to combine lines or other content. As we move into more dynamic content in the next section, its greater role will also become more apparent.

## Review

The flow of a story is movement from its beginning to end.

A line is a single section of content in an ink story.

We can use glue to combine multiple lines together to create a single
one.
