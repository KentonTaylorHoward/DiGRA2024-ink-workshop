# Unity: Loading and Parsing Story Data

## Loading Story Data

Loading story data into the Unity plugin requires two things: the story’s ".ink" file and the story’s exported ".json" file.

Story data can then be loaded via C#. Doing so requires including the ink runtime library:

```csharp
using Ink.Runtime;
```

ink stories are represented in C# using the Story variable type, like this:

```csharp
myStory = new Story (inkJSONasset.text)
```

In this example, we have created a variable called "myStory" and used the plugin functionality to load the ink story’s JSON file. The JSON
file is stored as a text asset within Unity and the story text can be displayed using Unity’s legacy UI text functionality.

Once loaded, the ".ink" file can be edited to quickly change the story itself, and story data, such as variables, functions, knots, and more
can be seen in the Unity inspector.

## Parsing Story Data

The plugin has a number of built tools for parsing story data within its custom inspector:

![ink-Unity Inspector Browser](../../../images/inkTools-Unity-Inspector.png 'ink-Unity Inspector')

This example shows the plugin’s Unity inspector. Several things an be seen here:

* The "Choices" drop down: This displays the current choices available within the game at a particular story state, with each choice displayed
as a clickable button.
* The "Story State" drop down: This drop down shows a few useful things about the story state, such as the story seed, that are typically used
with the "Save/Load" drop down (see below).
* The "Save/Load" drop down: This functionality allows for saving and loading a particular story state - story states are saved as a JSON file
and can be manually loaded using the drop down.
* The "Named Content" drop down: This displays any named content in the ink story, such as knots and stitches. Stitches are nested underneath
their related knots. Knots and stitches that have not been seen in the current story are marked as 0 and those that have been seen are marked
as 1 (or a number that corresponds to how many times that knot or stitch has been diverted to).
* The "Functions" drop down: This shows any functions in the ink story.
* The "Variables" drop down: This shows any variables in the story, the current value of that variable, and the variable type.
