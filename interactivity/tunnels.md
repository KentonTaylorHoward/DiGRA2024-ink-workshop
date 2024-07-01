# Tunnels

The use of knots and diverts can often create patterns where an author might need to move to a section and return without always knowing where the "return" place is in a story. To help with this, the ink narrative scripting language supports a concept known as a *tunnel*.

A tunnel is created with a divert followed by the name of a knot and another divert. When run, this creates a "tunnel" through the knot and
back to the starting place.

```ink
Start here,
-> section ->
and back again.

== section
and then this,
->->
```

In the previous example, the *section* knot includes a "double divert." This returns back to where the tunnel was created when encountered.

## Recurring Sections

Tunnels are especially useful in cases where knots might need to be revisited multiple times in a story. Because the tunnel will always
"return" back, the knot needs not know where the divert started.

```ink
VAR name = "Dan"

Hello, my name is <>
-> showName ->
<>. Did you get that?
The name is <>
-> showName ->
<>.

== showName
{name}
->->
```

In the previous example, the knot *showName* contains only a single line showing the value of the variable *name*. The use of the tunnels in the story allows for "going and returning" to the same knot multiple times.

For each usage, the story "returns" back to where the tunnel begins and makes its use invisible to others outside of the story.

## Review

Tunnels are an advanced pattern created from the use of diverts and knots.

The use of tunnels "go and return" from a knot as long as it includes the "double divert" usage.

For knots where the story might be visited multiple times, this is a useful pattern.
