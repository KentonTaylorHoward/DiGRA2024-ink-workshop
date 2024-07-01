# Example: Command-Line Banking

In this example, the [consola](https://github.com/unjs/consola) library is used to create a selection prompt for the user based on the JavaScript API from the [inkjs](https://github.com/y-lohse/inkjs) library. This example re-uses the **banking.ink** file from the tunnel version of its code.

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

**banking.js**

```javascript
// Import the readFileSync function from the fs module.
import { readFileSync } from 'fs';

// For the Story class, import the Story object from the inkjs module.
import { Story } from 'inkjs';

// Import the consola module.
import consola from "consola";

// Read the JSON file.
const json = readFileSync('./banking.json', 'UTF-8');

// Create a new Story object with the JSON content.
const inkStory = new Story(json);

/**
* Continue the story.
* @function continueStory
* @returns {void}
*/
function continueStory() {
   // Check if the next line of the story exists.
   if(inkStory.canContinue) {
       // Load everything up to the next weave.
       console.log(inkStory.ContinueMaximally());

       // Check if there are choices.
       if(inkStory.currentChoices.length > 0) {
           // Create a menu.
           createMenu();
       }
   } else {
       console.log('The End.');
   }
}

/**
* Create a menu.
* @function createMenu
* @returns {void}
*/
function createMenu() {
   // Create a menu.
   const menu = inkStory.currentChoices.map((choice, index) => {
       return { label: choice.text, value: index };
   });

   // Prompt the user to choose.
   consola.prompt("Choose:", {
       type: "select",
       options: menu
   }).then((choice) => {
       // Pick the choice.
       inkStory.ChooseChoiceIndex(choice);
       // Continue the story.
       continueStory();
   });
}

// Continue the story.
continueStory();
```
