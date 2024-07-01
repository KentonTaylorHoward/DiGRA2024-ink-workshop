# Alternatives

Flow moves line by line in an ink story. Content begins and then moves through to the end. Often, however, interactive stories are more than static content. They contain dynamic elements based on programmed rules.

In ink, dynamic content is created as part of a concept named *alternatives*. These create output based on rules where, potentially,
each flow through a story might be different. Alternative content might be shown to a reader.

Programmed rules are placed within curly brackets, `{ }`. To create alternatives, we include multiple possible elements between the bar
symbol, `|`.

There are multiple types of alternatives.

## Sequence

A *sequence* is a collection of elements where each is shown in order until the last.

```ink
Today is {Monday|Tuesday}
```

When run, the next element in the collection will be selected to generate story content - so in the example above, the reader would see
"Today is Monday" the first time the sequence is run and "Today is Tuesday" the second time. A sequence "ends" with the last element,
however, so if the reader visited that sequence a third time the reader would see "Today is Tuesday" again. See "Cycles" below for another way to address that.

## Cycle

A *cycle* is created like a sequence, but starts with an ampersand, `&`, inside the first curly bracket. When run, the collection will move to the next entry and then repeat the "cycle" when it reaches the end:

```ink
Today is {&Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday}
```

A cycle continues to repeat each time a reader encounters it, so in the previous example, the reader would see "Today is Monday" the first time the cycle runs, "Today is Tuesday" the second time, "Today is Wednesday", and then until Sunday is reached, after which the cycle
would reset.

## Once

The once alternative matches its name. It will only ever run once in a story. It is used with an exclamation mark, `!`.

```ink
The weather is {!raining|sunny|cloudy}.
```

A once alternative is similar to a sequence or a cycle; however, once all elements have been selected, it will show nothing. The alternative, including all its elements, will only be run once. This means that the example above would display "The weather is raining" the first time it was visited, "The weather is sunny" the second time, and "The weather is cloudy" the third time… but if it was visited a fourth time, we’d simply only get "The weather is".

## Shuffle

A *shuffle* appears like a sequence, but uses a tilde, `~`, inside the first curly bracket. A shuffle will select a random element from its
collection each time it is run.

```ink
Today is {~Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday}
```

In the previous example, the reader would see "Today is" and then a random day of the week. It is also valid to include multiple elements with the same exact name. This makes its selection more statistically likely.

## Combining Alternatives

Alternatives can be nested. In order to create more dynamic content, one form of an alternative can be embedded in another.

It is common, for example, to use nested shuffles to have random content generated at different depths or in connection with other, previous selections. Each of these is contained within its own set of curly brackets.

```ink
Today is a {~{~rainy |clear }Monday|{~stormy |sunny }Tuesday}.
```

In the previous example, one shuffle is nested inside another. The first shuffle selects between Monday or Tuesday. Next, the nested shuffle picks between rainy and clear-sky for Monday or stormy and sunny for Tuesday. This creates a situation where the reader could see many potential outcomes:

"Today is a rainy Monday"
"Today is a clear Monday"
"Today is a stormy Tuesday"
"Today is a sunny Tuesday"

## Multi-Line Alternatives

Alternatives can also be written in a more complex form using a colon with a hyphen per line per element. For example, to improve readability, a single line with many elements can become a multi-line alternative with one per line.

When using the multi-line form, the name of the type is used as part of the first line. These do not always match up exactly with the name of the type.

* Sequence: stopping
* Cycle: cycle
* Once: once
* Shuffle: shuffle

Using the multi-line version of a shuffle, it would appear as the following:

```ink
Today is <>{shuffle:
- Monday
- Tuesday
- Wednesday
- Thursday
- Friday
- Saturday
- Sunday
}
```

**NOTE:** We often use glue with multi-line alternatives because ink considers each entry as its own line.

## Review

Dynamic content is created using alternatives in ink. There are multiple
types.

A sequence is an alternative where each element is chosen in order and
"ends" with the last one.

A once alternative will move through its elements but only one single
time for each entry.

A cycle moves through each element and then back to the first again.

A shuffle selects an element randomly.

Alternatives can be nested together.

Each type of alternative can be written as a single line or across
multiple ones.
