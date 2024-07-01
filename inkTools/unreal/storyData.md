# Unreal: Loading and Parsing Story Data

**Before using the InkPot plugin, make sure to import at least one ".ink" file into the Content Browser.** Based on how the plugin is configured, it will automatically create the compiled JSON and make it an Inkpot Story Asset. There is no need to import any existing compiled JSON ink files, as these will be created by the plugin based on the imported file type.

When using the InkPot plugin, ink processing is part of a subsystem and must be invoked before any usage.

After opening a Blueprint for an Actor, search for "Get InkPot".

![Get InkPot](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-inkPot-GetInkPot.png 'Get InkPot')

After adding the subsystem node to the graph, pull off an event such as Event BeginPlay and search for the Begin Story node.

![Event BeginPlay](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-BeginStory.png 'Begin Story')

Attach the InkPot subsystem node as the target of the Begin Story node and then use the dropdown menu of the Inkpot Story Asset pin and select
any previously imported ".ink" files from the Content Drawer.

The Return output pin of the Begin Story node will contain an **Inkpot Story** object.

For example, the *Continue()* method of the general ink API can be invoked as a node of the same name as seen the in the following example:

![Continue Node Example](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-ContinueNode.png 'Continue Node Example')
