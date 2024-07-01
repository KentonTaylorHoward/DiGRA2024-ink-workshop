# Unity: Working with Story Data

**Note:** Make sure the ink-unity-integration plugin has been added to a project before using any code shown on this page.

The easiest way to work with existing or new ink code in Unity is to import the ink code as an asset. In Unity, this can be done using Assets
→ "Import New Asset..." and selecting the ink file. The file will then be automatically compiled and a JSON file with the same prefix will be
added. For example, if a *main.ink* file is imported, a *main.json* file will be created.

To use the C# API provided by the plugin, a compiled JSON file must be provided to the constructor method of the **Story** class. With the
plugin, this begins with a library containing all necessary classes for working with ink data: *Ink.Runtime*. This line should follow the
existing *UnityEngine* inclusion line:

```cs
using UnityEngine;
using Ink.Runtime;
```

In order to access a file, it must exist as an asset within the project. Because the ink-unity-integration plugin will automatically create the
necessary compiled JSON file, this can easily be used.

A common way for a C# scripting file in Unity to access an asset is to use the **TextAsset** class provided by Unity. This allows for
associating an asset in the Unity Editor with a cs field.

```cs
public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;
}
```

**Note:** There are multiple ways to access cs fields in Unity. Generally, if the field will only be used in the class and not shared
across other files, the attribute `[SerializeField]` can be used. This "shares" the field with itself and Unity only.

After associating a compiled JSON file in the Unity Editor with the updated field in the Inspector window in Unity, it can be accessed more
directly in the cs code.

The **TextAsset** class exposes a *text* property containing the loaded textual content as processed by Unity. In order to create a **Story**
object in ink, it needs the text of the compiled JSON file. Updating the code shown so far, the scripting component class might be the following.

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        Story s = new Story(jsonFile.text);
    }
}
```

In the previous example, beginning play will create a new **Story** object based on the text shared to the *inkExampleLoader* scripting
component class.

## "Is there more content?": *canContinue*

The first property to use when working with Unity data is named *canContinue*. This is a Boolean value. It will be *true* if there is at
least one more line in the story. It will be *false* if the story has ended or does not contain any lines.

```cs
// Create a story based on the compiled JSON text.
Story s = new Story(jsonFile.text);

// Check if more lines exist in the story.
if(s.canContinue)
{
    // Process lines.
}
```

## "What’s the next line?": *Continue()*

The *Continue()* method loads the next line in the story and returns any output it created as a result of its processing.

**Main.ink**

```ink
This has one line.
```

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // Check if more lines exist in the story.
        if(s.canContinue)
        {
            // Load the next line.
            string line = s.Continue();
        }
    }
}
```

In the previous example, the single line of the story will be loaded based on the use of the *Continue()* method.

## "What are the current tags?": *currentTags*

Tags are loaded on a per-line basis. The property *currentTags* will contain any tags, if any were found on the last line processed. In C#,
this property is a List.

```cs
// Were any tags loaded?
if(s.currentTags.Count > 0 )
{
    // Process tags.
}
```

In C#, the *Count* property of a List will contain the number of entries within the collection. To access the first entry, its index position can
be used. (In cs, the first position is the 0 index position.)

**Main.ink**

```ink
This has one line. #This is a tag.
```

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // Check if more lines exist in the story.
        if(s.canContinue)
        {
            // Load the next line.
            string line = s.Continue();

            // Were any tags loaded?
            if(s.currentTags.Count > 0 )
            {
                // Show in the Console the first tag.
                Debug.Log(s.currentTags[0]);
            }
        }
    }
}
```

In the previous example, the Console will show the text "This is a tag".

## "What are the next few lines?": *ContinueMaximally()*

There are often cases where all text up to the next weave is wanted. For these cases, the *ContinueMaximally()* method can be used. It will
continue to read lines until it encounters a weave.

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // Check if more lines exist in the story.
        if(s.canContinue)
        {
            // Load up to the next weave or end of story.
            string lines = s.ContinueMaximally();
        }
    }
}
```

In the previous example, multiple lines will be loaded by the use of the *ContinueMaximally()* method. It will always load up to the next weave
or end of the story, whichever comes first.

## "What are the current choices?": *currentChoices*

The property *currentChoices* is a List collection of all choices of the currently loaded weave. It will be populated through the previous uses
of the *Continue()* or *ContinueMaximally()* methods.

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // Check if more lines exist in the story.
        if(s.canContinue)
        {
            // Load up to the next weave or end of story.
            string lines = s.ContinueMaximally();

            // Are there any choices?
            if(s.currentChoices.Count > 0 )
            {
                // Process choices.
            }
        }
    }
}
```

As a List datatype in C#, each entry in the collection has an index position beginning with 0. In order to "choose" a particular entry, its
index position must be used.

## "How do I choose this choice?": *ChooseChoiceIndex()*

Based on the index position of the *currentChoices* property, the *ChooseChoiceIndex()* method accepts the number and "chooses" the
associated choice.

**Main.ink**

```ink
This is a line.

+ Choice 1
+ Choice 2
+ Choice 3
```

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // Check if more lines exist in the story.
        if(s.canContinue)
        {
            // Load up to the next weave or end of story.
            string lines = s.ContinueMaximally();

            // Are there any choices?
            if(s.currentChoices.Count > 0 )
            {
                // Pick the first choice.
                s.ChooseChoiceIndex(0);
            }
        }
    }
}
```

In the previous example, the use of the *ChooseChoiceIndex()* method will "choose" the first entry. Because of the use of the *Count*
property within the condition before its usage, this will prevent any issues with no choices existing or a weave not appearing at the current
point of the story progression.

## "What is the current value of a variable?": *variablesState*

The *variablesState* property contains an interface for accessing the internal values of a story. As soon as a **Story** object is created,
this property exists. To prevent some potentially complicated issues, all variables are pre-processed before the first use of the *Continue()*
and *ContinueMaximally()* methods.

As an interface, the *variablesState* property expects the name of a variable existing in the story. For example, if a variable is named
"name", it can be accessed directly.

**inkExampleLoader.cs**

```cs
using UnityEngine;
using Ink.Runtime;

public class inkExampleLoader : MonoBehaviour
{
    [SerializeField]
    TextAsset jsonFile;

    void Start()
    {
        // Create a story based on the compiled JSON text.
        Story s = new Story(jsonFile.text);

        // ink Variables are pre-processed.
        Debug.Log(s.variablesState["name"]);
    }
}
```

In the previous example, the ink variable *name* is accessed using the C# property *variablesState*.
