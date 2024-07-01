# Unreal: Working with Story Data

Much of the Unreal API matches the C# API provided by Inkle as part of the Ink-Unity-Integration plugin. However, as Unreal is more
event-driven and Blueprints node-based, there are some major differences, and there are some preferred patterns for Unreal noted on
this page.

## "Is there more content?": Can Continue

Mapped to Unreal, the Can Continue property in C# becomes a node returning a Boolean value. If the current story has at least one more
line of content, the Can Continue node’s return value will be *true*. Otherwise, it will be *false*.

![Can Continue](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-CanContinue.png 'Can Continue')

## "How do I load the next line?": Continue

The Continue node should always follow the use of the Can Continue node. If there are more lines, the Continue node will load the next line of
the story, process any variable changes, and update the current tags.

The target of the Continue node is the Inkpot Story produced from the Begin Story node.

![Continue Node](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-ContinueNode.png 'Continue Node')

## "What are the next few lines?": Continue Maximally

In cases where multiple lines should be loaded, the Continue Maximally node will load multiple lines up to the next weave or end of the story.

![Continue Maximally](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-ContinueMaximally.png 'Continue Maximally')

## "What are the current tags?": Current Tags

The Current Tags node will return the last tags loaded as an array. However, as tags are loaded on a per-line basis, Continue or
Continue Maximally nodes need to occur in the sequence before Current Tags to load.

![Current Tags](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-CurrentTags.png 'Current Tags')

## "What are the current choices?": Get Current Choices

The Get Current Choices node returns an array of Inkpot Choice objects. Similar to the C# API, each Choice object has text, which can be
accessed from the Get Text node.

![Current Choices](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-CurrentChoices.png 'Current Choices')

## "How do I pick a choice?": Choose Choice Index

The Choose Choice Index node allows for picking which choice, based on the index of the Current Choices array, should progress the story.

![Choose Choice Index](https://kentontaylorhoward.github.io/DiGRA2024-ink-workshop/images/inkTools-Unreal-ChooseChoiceIndex.png 'Choose Choice Index')
