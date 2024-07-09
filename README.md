# CMake Print Colored Text

A small helper you can include in your CMake build system to have colored text output, independent of the used Terminal or operating system.

## Contents
- [Description](#description)
- [Usage](#usage)
    - [Printing a message with one color](#printing-a-message-with-one-color)
    - [Printing only parts of the message with color and/or styles](#printing-only-parts-of-the-message-with-color-andor-styles)
    - [Using multiple colors in one message](#using-multiple-colors-in-one-message)

*See also: [License (zlib)](LICENSE.md)*

## Description
The normal `message(...)` command in CMake sadly doesnt support custom colors or styles for simple status messages. With this helper file you can print messages with colors or only have parts of the message printed with color, while the rest of the text in the same line is printed normally.
The helper **does not** use ANSI escape codes to print the colors and styles. It is fully compatible with every Terminal and every operating system.

## Usage
Include the file `colorFormatting.cmake` in your ***CMakeLists.txt***:
```
include("colorFormatting.cmake")
```

### Printing a message with one color
To print a whole message with one color and/or style you can use the `messageWithColor(...)` function:
```
messageWithColor(COLOR BLUE "My message with blue color")
```

To print a message using bold text use this argument:
```
messageWithColor(BOLD "My message in bold text")
```

The bold style and colors can also be combined:
```
messageWithColor(BOLD COLOR GREEN "My message in bold text and green color")
```

### Printing only parts of the message with color and/or styles
To print a part of the message with colors and/or styles, there is another function `colorFormatText(...)`. It takes the same arguments as `messageWithColor(...)` but doesnt print anything directly. Instead `colorFormatText(...)` sets a variable `COLOR_FORMATTED_TEXT`, which includes the formatted text that you can print urself. This way you can append unformatted text to formatted text:
```
# Formatted text is saved in COLOR_FORMATTED_TEXT
colorFormatText(COLOR GREEN "This is green:")

# Print the formatted text with unformatted text
message("${COLOR_FORMATTED_TEXT} This is without color")
```
**Result:**
<img src="/img/partial_color.png" alt="Partial Color"/>


## Using multiple colors in one message

## Supported colors and styles