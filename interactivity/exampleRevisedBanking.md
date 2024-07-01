# Example: Revised Banking

This new example uses tunnels instead of the previous use of knots and diverts. While the change is simple, the swapping of the explicit name of a knot for the "double divert" usage, there is one more change needed: a gather is needed as part of the weave within the *Menu* knot to "redirect" back to the knot, re-creating the menu. Otherwise, without the change, the tunnel would "return", the weave would close, and the story would end.

**banking.ink**

```ink
VAR money = 10
VAR stored = 0

-> Menu

== Menu
(Money: {money}   Stored: {stored})
+ [Withdraw]
    -> Withdraw ->
+ [Deposit]
    -> Deposit ->
+ [Exit Menu]
    -> END
-
-> Menu

== Withdraw
How much would you like to withdraw?
(Money: {money}   Stored: {stored})
+ {stored >= 1} [1]
    ~ stored = stored - 1
    ~ money = money + 1
+ {stored >= 5} [5]
    ~ stored = stored - 5
    ~ money = money + 5
+ {stored >= 10} [10]
    ~ stored = stored + 10
    ~ money = money + 10
+ {stored == 0} No stored money to withdraw.
-
->->

== Deposit
How much would you like to deposit?
(Money: {money}   Stored: {stored})
+ {money >= 1} [1]
    ~ money = money - 1
    ~ stored = stored + 1
+ {money >= 5} [5]
    ~ money = money - 5
    ~ stored = stored + 5
+ {money >= 10} [10]
    ~ money = money - 10
    ~ stored = stored + 10
+ {money == 0} No money to deposit.
-
->->
```
