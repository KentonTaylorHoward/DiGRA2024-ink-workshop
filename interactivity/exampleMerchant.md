# Example: Merchant

In this example, a simple merchant interaction is shown. Using multiple levels of a weave, a reader can select a branch and then see its
sub-branches. Selective output is used for the choice text to prevent it being part of the output. Gathering points are also used to simplify the output.

```ink
A merchant greets you as you enter the shop.

What can I get you today?

You see:
* [Tools]
    Interested in tools, eh?
    
    I have two types in stock.
    ** [Hammer]
        Great choice! Here's a hammer.
    ** [Shovel]
        Here's a perfect shovel for you.
* [Seeds]
    I have many different types of seeds to choose from today.
    
    What type of seed do you want?
    ** [Watermelon]
    ** [Sunflower]
    --
    Here are your seeds!
* [Books]
    Hmm. Sorry! It looks like I'm out of books for today. Try again tomorrow!
-
```
