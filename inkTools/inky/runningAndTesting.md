# Inky: Running and Testing

## Running

On Windows, you can run Inky by opening the "inky.exe" file in the installation folder you downloaded and unzipped.

On MacOS, use either the Spotlight Search and search for "Inky" or double-click on the Inky.app application directly from the Application
folder. (Remember, because it is a downloaded application, the first run must be done using the right-click → Open option and then confirming you want to open it.)

Unlike many other interactive fiction scripting engines, Inky is continually compiling: this means you do not need to write your code and
then compile it in order to test and debug.

## Testing

One of Inky’s most valuable features is the ability to both write ink code and see the results of that code immediately. Even more
importantly, you can play the resulting story immediately as well. Regular story text is displayed in black, while gray text indicates choices that can be clicked on.

Choices can be "rewound" by clicking the single arrow in the right pane that appears above the story, allowing you to easily test alternative choices. Clicking the double arrow restarts the story from the beginning.

Note that some functionality cannot be tested within inky. In particular, CSS styling, images, and most other visual features do not
function within inky and cannot be tested from within the editor. Using the "export for Web" or "export story.JS only" options are the best way to test these features.

The "story" menu also contains a number of tools that are useful for testing:

- Go to anything: This allows you to immediately jump to anything in the story, such as a knot, stitch, etc.
- Next issue: This allows you to jump to the next error or issue in the story (see "Debugging" below)
- Add watch expression: This allows you to track variables as you test the story
- Tags visible: This is turned on by default and allows you to see the tags in the story as you test it
- Word count and more: Provides an overview of various project data (such as word count, number of knots, number of choice, etc.)

Like many other editors, inky also provides both a content browser and an issue browser.

![Issue Browser](../../images/inkTools-Inky-IssueBrowser.png 'Reviewing Issues in Inky')

In the previous screenshot, a few things can be seen:

- The content browser on the left, which displays knots, stitches, and functions in the story.
- The issue browser in the top center, displaying the total number and type of errors in the story (the "1x" in the top center of the screen).
- A red "x" indicating the line of code that an error appears on.

Hovering over the issue browser provides a drop down that provides an error message for each issue.

Issues in inky can be categorized as follows:

- Errors: An ink story with any "red" error messages cannot be properly completed: these must be fixed before exporting the story to a playable version. The screenshot above shows an error.
- Warnings: A story can also have warnings, which look much like errors, but use orange indicators and error messages instead of red. Warnings do not always necessarily prevent story completion, but are an indication that something in the story may not be working properly or that something needs to be addressed.
  
Warnings look like the following:

![Warnings](../../images/inkTools-Inky-Warnings.png 'Warnings in Inky')

TODOs are user-defined. They work much like code comments in that they are ignored by the compiler and are used to write human readable information. You can create a TODO by typing TODO and then writing your information. Unlike code comments, TODOs appear in the issue browser in green.

![TODO](../../images/inkTools-Inky-TODO.png 'TODO Items in Inky')
