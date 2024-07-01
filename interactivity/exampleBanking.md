# Example: Banking

In this example, the amounts between the variables *money* and *stored* are changed based on conditional choices as part of multiple knots in the story. Depending on the action and knot, *Withdraw* or *Deposit*, a reader can exchange set amounts of 1, 5, or 10.

```ink
VAR money = 10
VAR stored = 0

-> Menu
== Menu
(Money: {money}   Stored: {stored})
+ [Withdraw]
    -> Withdraw
+ [Deposit]
    -> Deposit
+ [Exit Menu]
    -> END

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
- -> Menu

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
- -> Menu
```
