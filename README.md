# CMake Print Colored Text

A small and easy to use helper to include in your CMake build system to have colored text output, independent of the used Terminal or operating system.

<p align="center">
<img src="/img/title_img.png" alt="Title image" width="70%"/>
</p>

## Contents
- [Description](#description)
- [Usage](#usage)
    - [Printing a message with one color](#printing-a-message-with-one-color)
    - [Printing only parts of the message with color and/or styles](#printing-only-parts-of-the-message-with-color-andor-styles)
    - [Using multiple colors in one message](#using-multiple-colors-in-one-message)
- [Supported colors and styles](#supported-colors-and-styles)

*See also: [License (zlib)](LICENSE.md)*

## Description
The normal `message(...)` command in CMake sadly doesn't support custom colors or styles for messages. With this helper file you can print messages with colors, have multiple colors in one message, or only have parts of the message printed with color, while the rest of the text in the same line is printed normally.
This helper **does not** use ANSI escape codes directly to print the colors and styles. It is fully compatible with every Terminal and every operating system.

## Usage
Just copy the file `colorFormatting.cmake` next to your ***CMakeLists.txt*** and include it in your ***CMakeLists.txt***:
```cmake
include("colorFormatting.cmake")
```


### Printing a message with one color
To print the whole message with one color and/or style you can use the `messageWithColor(...)` function:
```cmake
messageWithColor(COLOR BLUE "My message with blue color")
```
#### Only bold
To print a message using bold text style and no color change use this argument:
```cmake
messageWithColor(BOLD "My message in bold text")
```

#### Color and bold
The bold style can be combined with colors:
```cmake
messageWithColor(BOLD COLOR GREEN "My message in bold text and green color")
```


### Printing only parts of the message with color and/or styles
To print a part of the message with colors and/or styles, there is another function called `colorFormatText(...)`. It takes the same arguments as `messageWithColor(...)`, but doesn't print anything directly.
Instead `colorFormatText(...)` sets the variable `COLOR_FORMATTED_TEXT`, which contains the formatted text that you can print yourself. This way you can append unformatted text to formatted text:

```cmake
# Formatted text is saved in COLOR_FORMATTED_TEXT
colorFormatText(COLOR GREEN "This is green:")

# Print the formatted text and append unformatted text
message("${COLOR_FORMATTED_TEXT} This is without color")
```

<h3>Result</h3>
<p align="center">
<img src="/img/partial_color.png" alt="Partial Color" width="70%"/>
</p>

### Using multiple colors in one message
To print a message with multiple colors and/or styles, you can use the `colorFormatTextAppend(...)` function. It takes the same arguments as `colorFormatText(...)` and doesn't print anything directly.
Instead it *appends* the given string to the `COLOR_FORMATTED_TEXT_COMBINED` variable, which includes all parts of the formatted text that you can print yourself:

```cmake
# Append multiple strings with different colors and styles
colorFormatTextAppend(COLOR RED "This is ")
colorFormatTextAppend(COLOR GREEN "a multicolor ")
colorFormatTextAppend(BOLD COLOR BLUE "message ")
colorFormatTextAppend(COLOR MAGENTA "test")

# Print the combined string with multiple colors
message("${COLOR_FORMATTED_TEXT_COMBINED}")
```

<h3>Result</h3>
<p align="center">
<img src="/img/multi_color_append.png" alt="Multi Color" width="70%"/>
</p>


## Supported colors and styles
| Color | Style |
|:-------:|:-------:|
| <table> <tr><td>NORMAL</td></tr> <tr><td>BLACK</td></tr> <tr><td>RED</td></tr> <tr><td>GREEN</td></tr> <tr><td>YELLOW</td></tr> <tr><td>BLUE</td></tr> <tr><td>MAGENTA</td></tr> <tr><td>CYAN</td></tr> <tr><td>WHITE</td></tr> </table> | <table> <tr><td>BOLD</td></tr> </table> |

**NOTE:** If an invalid color argument is passed to any of the above functions, the text will be printed without any color change. *No error message is printed.*
