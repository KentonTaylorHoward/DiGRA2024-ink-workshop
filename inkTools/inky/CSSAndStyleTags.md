# CSS and Style Tags

Using the "Export for Web" packaging process in Inky provides support for multiple tags with special meaning for the included JavaScript
processing.

## Changing Themes

The CSS provided in the packaging supports two theme options: dark and light. However, it is possible to change this programmatically using the `# theme` tag followed by a colon and then either the value "dark" or "light".

For example, to change the theme to dark, the tag formatting would appear as the following:

```ink
# theme: dark
```

## Clearing Previous Story Text

By default, the packaged story will show all text and scroll the page as the reader progresses the story. To "clear" the previous text of the story, the tag `# CLEAR` can be used.

```ink
# CLEAR
```

## Adding CSS Classes

While some styling is added to the packed story, it is possible to add CSS classes to the included *theme.css* file. These classes can then be applied programmatically using the `# CLASS` tag followed by a colon and then the name of a class from the *theme.css* file.

For example, assuming there was a class named *green*, the following line would have additional styling rules:

```ink
I am green text! # CLASS: green
```

## Including Images

While ink excels at working with text, it is possible to work with images using the "Export for Web" packaging. To use images, they should
be included in a relative path, either in the same directory or one in the same folder as the *index.html* file.

Images will always appear before the line containing the tag.

```ink
Suddenly, a cat appeared! # IMAGE: cat.jpeg
```

Using a relative path, images can also be organized into folders.

```ink
# IMAGE: images/cat.jpeg
```
