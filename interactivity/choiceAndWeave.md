# Choices and Weaves

Choices are a fundamental part of every interactive story. We often want to present the reader with the ability to choose between different
options to influence story outcomes.

## Weaves

A choice is created in ink using an asterisk, `*`, before a line. This is then presented as an option for a player to pick.

```ink
* Pick me!
* No, pick me!
* No, this one!
```

A collection of choices is named a *weave*. By default, when a player encounters a weave, whatever option they chose becomes a permanent part of their experience. This also becomes part of the output.

Each choice is considered a potential different branch of the overall story. This allows authors to create a *branching narrative* experience where, depending on the choice, the story branches in different ways.

Any line following a choice becomes part of its branch. When the option is chosen, it will become part of the next part of the flow of the
story.

```ink
* Branch A
This is some content!
* Branch B
This is some content!
* Branch C
This is some content!
```

In the previous example, each choice creates a branch with its own content.

To help human readability, it is recommended to add a tab to each line under a choice.

```ink
* Branch A
    This is some content!
* Branch B
    This is some content!
* Branch C
    This is some content!
```

Choices can be nested, Each new level of a weave begins with a new asterisk. For example, the first level has one and the second two.

```ink
* Branch A
    ** Sub-Branch AA
    ** Sub-Branch AB
* Branch B
    ** Sub-Branch BA
    ** Sub-Branch BB
* Branch C
    ** Sub-Branch CA
    ** Sub-Branch CB
```

Because each choice is its own branch, the next level of the weave is only active if the previous level of the branch was chosen. In the
previous example, the sub-branch AB can only be accessed if the branch A was previously chosen.

## Gathering together

Increasing the number of choices and sub-choices can quickly create a large number of branching paths, each requiring more content. To
partially solve this issue, ink has the concept of a *gathering point* with the minus sign, `-`.

```ink
* Branch A
    ** Sub-Branch AA
    ** Sub-Branch AB
* Branch B
    ** Sub-Branch BA
    ** Sub-Branch BB
* Branch C
    ** Sub-Branch CA
    ** Sub-Branch CB
- No matter what is selected, readers will end up here.
```

In the previous example, the gathering point matches the first level of the weave. The reader will always end up at the gathering point.

Like extra asterisks for additional levels of a weave, additional minus symbols can be used to match the same level of the weave to "gather" at the point within a larger branching structure.

```ink
* Branch A
    ** Sub-Branch AA
    ** Sub-Branch AB
    -- Gathering Point for Branch A
* Branch B
    ** Sub-Branch BA
    ** Sub-Branch BB
    -- Gathering Point for Branch B
* Branch C
    ** Sub-Branch CA
    ** Sub-Branch CB
    -- Gathering Point for Branch C
- Gathering Point for Weave
```

In the previous example, choosing a branch and then sub-branch will show the output of the choice, the gathering point of the internal weave, and then the weave of the larger weave.

Gathering points are a powerful way of providing choices, allowing players to select them, and then collapsing a weave from a more complex
branching structure into a simpler one.

## Selective output

By default, the text of each choice becomes part of the output when the player selects it. To prevent this from happening, the text can be
placed within square brackets, `[ ]`. This is known as *selective output.*

```ink
* [One]
* [Two]
* [Three]
```

In the previous example, regardless of what the reader chooses, no output will be created.

## Review

Allowing the reader to influence the story is known as a choice in ink.

One or more choices is known as a weave.

Weaves can be nested together with each branch unlocking its own sub-branches.

By default, the text of each choice is added to the output. Using square brackets around the text creates selective output, showing the text of the choice but not adding it to the output.
