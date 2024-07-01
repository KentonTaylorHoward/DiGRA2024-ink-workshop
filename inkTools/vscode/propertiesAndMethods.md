# Node.js + JavaScript API: Useful Properties and Methods

Working efficiently with the inkjs API means understanding how an ink story works and what is part of the overall API. Stories in ink are processed on a line-by-line basis until the end. In the inkjs API, there are multiple properties and methods for determining if more content exists, what current tags are loaded, and how to process either the next line or up to the next weave encountered.

## "Is there more?": *canContinue*

The first property to use when processing an ink story is *canContinue*.
This is a Boolean value and reports if more lines exist in the story.

```javascript
// Import the readFileSync function from the fs module.
import { readFileSync } from 'fs';
// For the Story class, import the Story object from the inkjs module.
import { Story } from 'inkjs';

// Read the JSON file.
const json = readFileSync('./example.json', 'UTF-8');

// Create a new Story object with the JSON content.
const inkStory = new Story(json);

// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Process the next and potentially future lines of the story.
}
```

In the previous example, a condition statement is used to test if the loaded story contains any lines using the *canContinue* property.

## "Load next line": Continue() method

In many cases, loading only a single line of possible output is needed. For this, the *Continue()* method can be used.

```javascript
// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load and return the next line of the story.
   const line = inkStory.Continue();
}
```

In the previous, simplified example, the *Continue()* method is used to load, process, and return the output of the next single line of ink code.

## "What are the current tags?": *currentTags*

Assuming at least one line of a story has been loaded, the *currentTags* property will be populated.

```javascript
// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load and return the next line of the story.
   const line = inkStory.Continue();

   // Access current tags.
   const tags = inkStory.currentTags;
}
```

In JavaScript, this is an array, and its *length* property can be used to check how many tags are currently loaded from the last line.

```javascript
// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load and return the next line of the story.
   const line = inkStory.Continue();

   // Access current tags.
   const tags = inkStory.currentTags;

   // Were there any tags?
   if(tags.length > 0) {
       // Process the tags.
   }
}
```

In the previous example, the *tags* variable contains any tags loaded as an array and its own property, *tags.length*, can be used to detect if any tags exist from the last line loaded.

## "What is the current value of a variable?": *variablesState*

Each ink story is a container with its own variables and other data. In order to access and potentially change the value of a variable, the *variablesState* property is used. In JavaScript, this is defined as a proxy. To access the value of a variable, its name is needed.

To prevent some complicated issues from happening, the loading of a story will also trigger the processing of any variables. If a variable exists in the ink story, it can be immediately accessed.

**main.ink**

```ink
VAR name = "Dan"
This is output.
This is another line.
```

**index.js**

```javascript
// Create a new Story object with the JSON content.
const inkStory = new Story(json);

/**
* Variables are pre-processed in ink.
*
* Once a story is loaded, the variablesState object is available.
*/
const name = inkStory.variablesState["name"];

// Show the value, which is "Dan".
console.log(name);
```

The immediate availability of variables via the *variablesState* proxy also means any values can be changed before processing any lines as well.

**main.ink**

```ink
VAR name = "Dan"
The name is {name}.
```

**index.js**

```javascript
// Read the JSON file.
const json = readFileSync('./main.json', 'UTF-8');

// Create a new Story object with the JSON content.
const inkStory = new Story(json);

/**
* Variables are pre-processed in ink.
*
* Once a story is loaded, the variablesState object is available.
*
* Overwrite the name variable with a new value.
*/
inkStory.variablesState["name"] = "Taylor";

// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load and return the next line of the story.
   const line = inkStory.Continue();

   // Print the line to the console.
   // This will produce "The name is Taylor."
   console.log(line);
}
```

As the previous example illustrates, it is possible to overwrite values in a story based on the name of variables before any lines are processed.

## "Load all lines up to the next weave": *ContinueMaximally()*

In cases where all possible output up to the next weave is wanted, the *ContinueMaximally()* method will "continue" until an action is taken as part of a weave.

**main.ink**

```ink
This is a line.
This is another line.
+ Choice 1
+ Choice 2
+ Choice 3
```

**index.js**

```javascript
// Create a new Story object with the JSON content.
const inkStory = new Story(json);

// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load everything up to the next weave.
   const line = inkStory.ContinueMaximally();

   // Print multiple lines to the console.
   console.log(line);
}
```

In the previous example, the use of the *ContinueMaximally()* method will load any and all lines up to the next weave.

## "What are the current choices?": *currentChoices*

Assuming a weave has been encountered via either the *Continue()* or *ContinueMaximally()* methods, the property *currentChoices* will be populated with all choices of the current weave.

**main.ink**

```ink
This is a line.
This is another line.
+ Choice 1
+ Choice 2
+ Choice 3
```

**index.js**

```javascript
// Create a new Story object with the JSON content.
const inkStory = new Story(json);

// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load everything up to the next weave.
   const line = inkStory.ContinueMaximally();

   // Print the number of choices in the current weave.
   // This will print: 3
   console.log(inkStory.currentChoices.length);
}
```

In the previous example, the *currentChoices* property will be populated with three entries based on the number of choices in the currently loaded weave.

Each choice within the *currentChoices* property contains individual objects. In order to access its output, its *text* property must be used.

```javascript
// Create a new Story object with the JSON content.
const inkStory = new Story(json);

// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load everything up to the next weave.
   const line = inkStory.ContinueMaximally();

   // For each choice in the story, print the text of the choice.
   inkStory.currentChoices.forEach(choice => {
       console.log(choice.text);
   });
}
```

In the previous example, the text of each choice will be printed to the console.

## "How do I pick a choice?": *ChooseChoiceIndex()*

If a weave has been loaded via the *Continue()* or *ContinueMaximally()* methods, the *currentChoices* property will contain entries matching the choices of the weave. Picking on these choices requires the use of the *ChooseChoiceIndex()* method with an index position matching an entry. (In JavaScript, arrays begin at an index position of 0 for the first
entry.)

```javascript
// Check if the next line of the story exists.
if(inkStory.canContinue) {
   // Load everything up to the next weave.
   const line = inkStory.ContinueMaximally();

   // Pick the first choice.
   inkStory.ChooseChoiceIndex(0);
}
```

In the previous example, the use of the *ChooseChoiceIndex()* method picks the first entry matching those found in the *currentChoices* property.
