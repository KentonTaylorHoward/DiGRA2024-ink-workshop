# Thinking of Stories as Containers

When ink is combined with another tool, a runtime is provided to access its data. When loaded, each compiled JSON file becomes a **Story**
object with its own methods or functions, depending on the programming language, for accessing data.

When understood this way, each story is a "container" with its own variables, knots, and progression. Because each story is its own
**Story** object, they are run separately depending on how they are used in connection to other code.

## Local Progression, Global Variables and Knots

At any point in an ink story, any existing value of a variable or section of a story diverted to during its progression. This makes them
*global* to the story itself. They can be accessed from any point.

Considered as part of a **Story** object within a programming language, this means each story’s variables and knots can also be accessed
externally because of this global nature. When used with other tools, this pattern can be very powerful. For example, multiple stories can be loaded and progressed at the same time, accessing the internal values of their individual variables to compare them.

## Review

Each ink story is its own "container." It holds all of its variables, knots, and lines.

When considered as a **Story** object, any data can be accessed or even potentially changed using methods or functions, depending on the
programming language.
