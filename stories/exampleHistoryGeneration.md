# Example: History Generation

In this example, multiple variables are created with default values at the beginning of the story. (Remember, variables must be created with values!) The values of the variables are then re-assigned using the result of shuffle alternatives. These random values are then shown to the reader by surrounding each variable in curly brackets as part of a line creating output.

```ink
VAR years = 0
VAR prefix= ""
VAR suffix = ""

// Assign random years.

~ years = "{~10|20|30|40|50|60|70}"

// Assign random prefix.

~ prefix = "{~Ste|Rea|Ult}"

// Assign random suffix.

~ suffix = "{~Union|Republic|Kingdom}"

The {prefix} {suffix} has stood for {years} years.
```
