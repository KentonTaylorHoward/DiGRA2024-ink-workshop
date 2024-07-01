# Weaves and Loops

Through using weaves in ink, choices can be provided to a reader and the flow of a story potentially branched. With diverts, a story can have different sections and, with stitches, subsections. Combining these two concepts opens up a pattern of creating a loop where a reader can move between sections containing weaves.

Previously, when describing choices and weaves, the phrase "a permanent part of their experience" was used to describe how choices influence output. If a reader revisits a weave they have previously visited during the flow of a story, this will be true by default.

At first glance, the following code would seem to make sense but actually creates a major issue.

```ink
-> menu1

== menu1
* A
    ** AA
    ** AB
    -- -> menu1
* B
    ** BA
    ** BB
    -- -> menu1
```

In the previous code, each loop back to the *menu1* knot will show a reduced set of choices for the weave. Anything previously selected will be removed, as it is now part of the previous flow of the story. Eventually, the reader will encounter an issue: once the branches have been exhausted, the story will crash. Without another choice within the weave to show the reader, the story will get confused about what to do next.

## Sticky Choices

By default, choices created with an asterisk are "permanent" to the flow of a story. To create recurring choices, what is described as *sticky choices*, we can use the plus symbol, `+`.

```ink
-> menu

== menu
+ Choice 1
    -> menu
+ Choice 2
    -> menu
+ Leave Menu
    -> END
```

In the previous example, internal loops are created using sticky choices. The result of either *Choice 1* or *Choice 2* will divert to
the *menu* knot, creating a loop. Finally, to end the loop, the *Leave Menu* choice can be picked, diverting to the END knot.

Text is not the only part of a story affected by conditions. It is also possible to make choice availability based on conditions within a weave as well.

## Conditional Choices

A choice becomes conditional if it contains curly brackets. If the condition is true, the choice will be shown. Otherwise, it will be
removed from the weave.

In cases where sections of a story might be revisited after values change, conditional choices can allow for more dynamic shaping of weaves
based on the current values within the flow of a story.

```ink
VAR amount = 10

->test
== test
+ {amount >= 1} Decrease (Current amount: {amount})
    ~ amount = amount - 1
    -> test
+ {amount <= 10} Increase (Current amount: {amount})
    ~ amount = amount + 1
    -> test
+ End Loop
    -> END
```

In the previous example, the *Decrease* and *Increase* sticky choices only appear if the value of the variable *amount* matches a specific
range. As mechanics for an interactive story, this keeps the value within a range of a minimum of 0 and a maximum of 10 by removing a
choice conditionally.

## Review

Choices created using an asterisk can only be selected once.

Sticky choices, those using the plus symbol, "stick around" if the section of the story is ever revisited.

When using loops in ink, it is often important to make sure at least one sticky choice appears within a weave to prevent the story from crashing.

Conditional choices can affect the number of choices in a weave. These are most useful within looping structures in a story where previous
values may have changed between loops.
