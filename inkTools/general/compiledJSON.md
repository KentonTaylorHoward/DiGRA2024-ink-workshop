# ink and Compiled JSON

When working with the narrative scripting language ink, it exists in two forms. The first is the "ink" form as human-readable text. This can be easily opened and edited. Data in this format is often saved as part of files ending in ".ink".

Stories in ink also exist as what is called "compiled JSON." In order to run a story, it must be converted into JavaScript Object Notation (JSON) as part of a "compiled" form. Depending on the tool and platform, this process can be slightly different, but the result is the same: a computer-readable format for running the story.

**In order to be run, there must exist a compiled JSON form of the story**. This is what is understood by other tools in order to process
its output, tags, and understand the values of variables. This data is saved as part of a ".json" file.
