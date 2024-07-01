# Saving and Comparing Data

Many interactive stories have values shared across sections or as input from a reader. In ink, we can save and manipulate data using
*variables.*

Variables are created using the keyword `VAR`, written in capital letters, followed by the name of the variable, an equal sign and some value as a single line. Borrowing from more general programming terms, this is known as *assignment*. A variable is being assigned a value.

**INFO:** ink supports many types of values including *integers* (whole numbers), *floating point* (decimal), and *strings* (collections of
letters, numbers, or special symbols surrounded by quotation marks). Single quotation marks cannot be used.

```ink
VAR exampleInteger = 5
VAR exampleFloatingPoint = 3.14
VAR exampleString = "Hi!"
```

Variables have multiple rules defining how they are used:

- The name of a variable can only contain letters, numbers, and the underscore. Spaces and special symbols cannot be used.
- Variables must be created with a value. They cannot be "empty."
- Variables cannot share names in a story.
- Variables are global to a story. Once created, they can be accessed anywhere.

When using variables in ink, it is strongly recommended to create all variables at as near the beginning of the story as possible. In much
more complex stories, it is not uncommon to have a dedicated section of a story for creating variables and assigning their initial values.

The use of the VAR keyword does not add the output of a story. To show the value of a variable, additional symbols are required.

## Showing values

The value of a variable can become part of story output by including the name of a variable within curly brackets by itself:

```ink
VAR name = "Jane"
Hi, my name is {name}!
```

In the previous example, the line containing the variable will not produce output.

## Conditional text

ink supports the use of comparisons between the value of a variable and some other value. This is known as *conditional text*.

To test the value of a variable, the comparison and possible result should be placed within curly brackets, `{}`, with a colon following the comparison and what should run or be shown after the colon inside the curly brackets.

Comparisons can be performed using the following symbols and combinations:

- Greater than: &gt;
- Greater than or equal to: &gt;=
- Less than: &lt;
- Less than or equal to: &lt;=
- Equality: ==
- Inequality: !=

When using a comparison including the value of a variable, the variable must exist before the line containing the comparison.

```ink
// Create variables before any other content.
VAR health = 10

// Conditional text.
// If the value of 'lives' is greater
// than 5, show some text.
{health > 5: You are very healthy!}
```

In the previous example, because the value of *health* is greater than the number 5, "You are very healthy" will be shown to the reader.

## Multi-line conditions

Similar to alternatives, conditional text can also be written across multiple lines. This pattern follows the same form of conditional text
but combines with the approach of multi-line alternatives where each condition becomes its own line beginning with a hyphen.

When using multiple conditions, each will run in order from top to bottom. It is recommended, when using this pattern, to have the last
condition be a catch-all.

```ink
VAR health = 4

// Conditional text can extend multiple lines.
{
- health > 8: You are very healthy!
- health > 5: You are mostly healthy.
- health <= 4: You are unwell.
}
```

In the previous example, each comparison will be run in turn with the last one generating output: "You are unwell."

## Updating values

Updating the existing value of a variable can happen at any point in a story after the variable has been created.

To change the value of a variable, use a tilde, `~`, followed by an assignment operation using the name of the variable and a new value. Any line using a tilde will not add to the output of a story.

```ink
VAR name = "Dan"

Hi, my name is {name} and <>
~ name = "Taylor"
My name is {name}.
```

In the previous example, the variable has the value "Dan". Next, the value of the variable is updated and becomes "Taylor". This creates, ultimately, the output "Hi, my name is Dan and my name is Taylor".

**Tip:** The use of the tilde, `~`, is an exception to programming operations using curly brackets.

## Saving the outcome of an alternative

The result of an alternative can be saved in a variable. However, the variable must exist *before* the use of the alternative and assignment. It is common to assign a default value and then update the variable on a later line of the story.

```ink
VAR day = ""

~ day = "{~Monday|Tuesday|Wednesday|Thursday|Friday}"

Today is {day}.
```

In the previous example, the use of double quotation marks appears around the use of a shuffle. This converts the resulting text into a
string value before it is assigned to the variable day. The reader would see a random day, such as "Today is Wednesday," and the `Wednesday` outcome would be saved.

## Review

Variables are created using the keyword VAR followed by the equal sign
and some value.

The value of a variable can be shown to a reader by placing it inside
curly brackets.

Variables can be compared using conditional text. This can produce
dynamic content through reacting to the value of variables.

Multiple conditional text lines can be combined within a single set of
curly brackets with each comparison and output as its own single
beginning with a hyphen.

The value of a variable can be updated using a line beginning with a
tilde.

The outcome of an alternative can be saved as the value of a variable.
