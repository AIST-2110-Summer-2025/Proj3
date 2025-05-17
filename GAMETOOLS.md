# `gametools.py` Basics

The file `gametools.py` is a Python module that contains functions that make
your games display text in a nicely formatted (and *colorful*). It also provides
convenience functions for getting user input.

The functions in this module _**<u>must</u>**_ be used in your game.

## Functions

  - `write()`

    Display a passage of text or a list of items to the screen.

    This is similar to python's built-in print() function, but with a lot of
    extra bells and whistles.

    In addition to allowing for colored and formatted text, it will
    automatically wrap long passages of text to fit properly in the terminal
    window.

    It will also behave differently depending on whether it is displaying a
    single string of text or if the content is a list of strings.

    Most of the time you will call this method with a passage of text to be
    printed to the screen. Text can contain markup to alter the color and
    display characteristics, but is otherwise just a string.

    However, if you pass a list of strings, write() will process each item in
    the list as though it was passed individually to the write function.
    Additionally, if you set either the bulleted or numbered arguments to True
    write() will prefixing each item with a bullet or an automatically
    incremented number.
    
    You can pass an optional, named argument to specify the display style of the
    passage (described elsewhere).

    You can pass an optional named arguments to set a `prefix` string to prepend
    to the first line in the text passage and an `indent` string to prepend to
    all following lines. This is a more flexible alternative to setting bulleted
    = True, which just sets prefix to `" • "` and indent to `"    "`.

    Additionally, you can pass an optional, named argument to specify whether to
    justify the text in the passage. Valid values are "left" (default),
    "center", "right" and "full".

    Finally, you can pass a boolean argument specifying that you wish to draw a
    box around the content.

  - `write_md()`
   
    This is a special version of the write() function that accepts a string of
    markdown-formatted text. It uses a pre-defined set of styles to display the
    text to the screen in a consistent format.

    The optional named style argument can be passed to set the foreground and
    background colors.

    Setting boxed=True will display the content inside of a box.

  - `get_input()`

    Prompt a user for input and optionally validate it.

    If a list of choices is provided, a user's input will be validated to insure
    it is one of the members of the list.

    By default, if the list of choices is provided, these are displayed to the
    user. This behavior can be altered by setting the show_choices named
    argument to False.

    If no choices are provided, by default any text, including an empty string,
    are allowed. To require the user to enter something, you can specify a
    min_length using the optional named argument.

  - `get_choice()`

    Allow the user to select from a list of choices.
    
    The user is presented with a navigable list of choices. Using the up/down
    arrow keys, the user selects an item and presses Enter to select.

    The _index_ of the selected item is returned.

    If desired, specific indexes can be hidden from a user. This may be useful
    if you wish to use the same get_choice() and if/elif/else logic, but you
    need to alter the available choices for a user based on some game state
    change.
    
  - `clear()`

    Clears the terminal window.
  
  - `pause()`

    Displays a message and waits for a user to press any key.

    You can customize the message displayed to the user. By default it is "Press
    any key to continue...".

    This function takes optional, named arguments for style and justify that are
    identical to those used in write().

  - `spin()`

    Sleep for a specified period, optionally showing a message and animation.

    Neither the message nor the spinner arguments is required. If both are
    omitted, this behaves identically to time.sleep().

    If a message argument is supplied, then the message will be displayed until
    the timer expires, at which time it will disappear.

    If a spinner argument is supplied, it must be one of the valid spinner
    values enumerated elsewhere. The spinner animation will display to the left
    of any message and will also disappear once the timer expires.

  - `set_terminal_width()`

    Gametools will automatically manage wrapping of long paragraphs for you. By
    default, wrapping occurs at the full width of the terminal up to a max of
    120 characters. Generally anything wider than this is more difficult to
    read, but if needed you can pass a value to this function to change this
    default width. Calling it with no arguments will reset it to the default.

    > _This is unlikely to be used, so it is not imported for you by default._

## Rich Strings

To make your games even more fun and visually stimulating for players, gametools
allows you to change the colors and modify the display characteristic of your
text. The valid modifiers and colors are all listed below.

You can either embed codes to your strings somwhat similar to HTML. Or you can
add an argument to the write() function that will modify the display all text.

### Usage in string:

Color and display modifiers are embedded in strings by enclosing the text that
you want to modify inside of tags. Tags are delimited using square brackets and
always come in opening and closing pairs.

Opening tags contain the colors and modifiers; e.g., `[yellow]` or `[bold]`.
Closing tags contain simply a forward slash, i.e., `[/]`. Colors and modifiers
can be combined into a single opening tag. Most of the modifiers can be provided
using a full name or a shortened single letter (see the full list of modifiers
below).

> Note that if your text is intended to contain an open square bracket, then you
> should "escape" this bracket with a backslash, i.e. `\[`.

This syntax works for strings in all gametools functions that display text
except for write_md(), as this markup is not "standard" markdown.

Basic usage:
``` python
write("You see [bold]two[/] [italic]extremely[/] ugly shoes on the ground.")
```

Short modifiers:
``` python
write("You see [b]two[/] [i]extremely[/] ugly shoes on the ground.")
```

Combined modifiers:
``` python
write("You see two [bold italic]extremely[/] ugly shoes on the ground.")
```

Colors can be added by themselves or combined with other modifiers. Colors are
specified in the form `foreground` or `on background` or `foreground on
background`.

Example foreground colors:
``` python
write("You see both a [bright_red]red shoe[/] and a [bright_blue]blue shoe[/].")
```

Example background colors (combined with a bold modifier):
``` python
write("You see both a [bold on red]red shoe[/] and a [bold on blue]blue shoe[/].")
```

Example combined foreground, background and modifiers:
``` python
write("I am [bold yellow on green]SICK[/] of seeing shoes.")
```

### Usage in write function:

You can style an entire passage in either the write() or write_md() function by
passing a "named argument". See the following example.

``` python
write("The quick fox lazy dog whatever blah", style="white on red")
```

And yes, you can do both:

``` python
write(
    "The [i]quick[/] [b]red[/] fox jumps over the [b u i]lazy[/] dog",
    style="white on red"
)
```

### EMOJIS

You can also embed emojis in your text by adding `:emoji_name:` to any string
that you display using the any of the gametools functions.

  - `:smile:`
  - `:warning:`
  - `:unlocked:`
  - `:thumbs_up:`
  - There are many hundreds of them...
    + list them using the following command at the terminal:
        `python -m rich.emoji`

For example:
``` python
write(":unlocked: The door is now unlocked.")
```

And of course you can combine and nest everything to the extent of your
imagination.

``` python
write(
    "[bold white on red][blink]:danger:[/] !!! WARNING !!! [blink]:danger:[/][/]"
)
```


### MODIFIER REFERENCE

  - `bold` or `b`
  - `italic` or `i`
  - `reverse` or `r`
  - `strike` or `s`
  - `underline` or `u`
  - `blink` ( *doesn't work on Codespaces* )


### COLORS

#### Safe (ANSI) Colors
  - black
  - red
  - green
  - yellow
  - blue
  - magenta
  - cyan
  - white
  - bright_black
  - bright_red
  - bright_green
  - bright_yellow
  - bright_blue
  - bright_magenta
  - bright_cyan
  - bright_white


#### All (X11) Colors
|                 |                 |                 |                 |                 |
|-----------------|-----------------|-----------------|-----------------|-----------------|
| aquamarine1     | aquamarine3     | black           | blue            | blue1
| blue3           | blue_violet     | bright_black    | bright_blue     | bright_cyan
| bright_green    | bright_magenta  | bright_red      | bright_white    | bright_yellow
| cadet_blue      | chartreuse1     | chartreuse2     | chartreuse3     | chartreuse4
| cornflower_blue | cornsilk1       | cyan            | cyan1           | cyan2
| cyan3           | dark_blue       | dark_cyan       | dark_goldenrod  | dark_green
| dark_khaki      | dark_magenta    | dark_olive_green1 | dark_olive_green2 | dark_olive_green3
| dark_orange     | dark_orange3    | dark_red        | dark_sea_green  | dark_sea_green1
| dark_sea_green2 | dark_sea_green3 | dark_sea_green4 | dark_slate_gray1 | dark_slate_gray2
| dark_slate_gray3| dark_turquoise  | dark_violet     | deep_pink1      | deep_pink2
| deep_pink3      | deep_pink4      | deep_sky_blue1  | deep_sky_blue2  | deep_sky_blue3
| deep_sky_blue4  | dodger_blue1    | dodger_blue2    | dodger_blue3    | gold1
| gold3           | gray0           | gray100         | gray11          | gray15
| gray19          | gray23          | gray27          | gray3           | gray30
| gray35          | gray37          | gray39          | gray42          | gray46
| gray50          | gray53          | gray54          | gray58          | gray62
| gray63          | gray66          | gray69          | gray7           | gray70
| gray74          | gray78          | gray82          | gray84          | gray85
| gray89          | gray93          | green           | green1          | green3
| green4          | green_yellow    | grey0           | grey100         | grey11
| grey15          | grey19          | grey23          | grey27          | grey3
| grey30          | grey35          | grey37          | grey39          | grey42
| grey46          | grey50          | grey53          | grey54          | grey58
| grey62          | grey63          | grey66          | grey69          | grey7
| grey70\         | grey74          | grey78          | grey82          | grey84
| grey85          | grey89          | grey93          | honeydew2       | hot_pink
| hot_pink2       | hot_pink3       | indian_red      | indian_red1     | khaki1
| khaki3          | light_coral     | light_cyan1     | light_cyan3     | light_goldenrod1
| light_goldenrod2|light_goldenrod3 | light_green     | light_pink1     | light_pink3
| light_pink4     | light_salmon1   | light_salmon3   | light_sea_green | light_sky_blue1
| light_sky_blue3 | light_slate_blue| light_slate_gray| light_slate_grey| light_steel_blue
| light_steel_blue1| light_steel_blue3| light_yellow3 | magenta         | magenta1
| magenta2        | magenta3        | medium_orchid   | medium_orchid1  | medium_orchid3
| medium_purple   | medium_purple1  | medium_purple2  | medium_purple3  | medium_purple4
| medium_spring_green | medium_turquoise | medium_violet_red | misty_rose1 | misty_rose3
| navajo_white1   | navajo_white3   | navy_blue       | orange1         | orange3
| orange4         | orange_red1     | orchid          | orchid1         | orchid2
| pale_green1     | pale_green3     | pale_turquoise1 | pale_turquoise4 | pale_violet_red1
| pink1           | pink3           | plum1           | plum2           | plum3
| plum4           | purple          | purple3         | purple4         | red
| red1            | red3            | rosy_brown      | royal_blue1     | salmon1
| sandy_brown     | sea_green1      | sea_green2      | sea_green3      | sky_blue1
| sky_blue2       | sky_blue3       | slate_blue1     | slate_blue3     | spring_green1
| spring_green2   | spring_green3   | spring_green4   | steel_blue      | steel_blue1
| steel_blue3     | tan             | thistle1        | thistle3        | turquoise2
| turquoise4      | violet          | wheat1          | wheat4          | white
| yellow          | yellow1         | yellow2         | yellow3         | yellow4


### Spinners

The following is a list of all valid spinner string values that can be passed to
the spin() function. Most create animations that are only one character wide. A
few create more elaborate, multi-character animations.

It is impractical to render animations in the browser, so "playing" with each of
these is a good option. But you can also get a feel for the animations by examining each "frame" of each of the animations in the [source code](https://github.com/Textualize/rich/blob/master/rich/_spinners.py).

  - "aesthetic"
  - "arc"
  - "arrow"
  - "arrow2"
  - "arrow3"
  - "balloon"
  - "balloon2"
  - "betaWave"
  - "bounce"
  - "bouncingBall"
  - "bouncingBar"
  - "boxBounce"
  - "boxBounce2"
  - "christmas"
  - "circle"
  - "circleHalves"
  - "circleQuarters"
  - "clock"
  - "dots"
  - "dots10"
  - "dots11"
  - "dots12"
  - "dots2"
  - "dots3"
  - "dots4"
  - "dots5"
  - "dots6"
  - "dots7"
  - "dots8"
  - "dots8Bit"
  - "dots9"
  - "dqpb"
  - "earth"
  - "flip"
  - "grenade"
  - "growHorizontal"
  - "growVertical"
  - "hamburger"
  - "hearts"
  - "layer"
  - "line"
  - "line2"
  - "material"
  - "monkey"
  - "moon"
  - "noise"
  - "pipe"
  - "point"
  - "pong"
  - "runner"
  - "shark"
  - "simpleDots"
  - "simpleDotsScrolling"
  - "smiley"
  - "squareCorners"
  - "squish"
  - "star"
  - "star2"
  - "toggle"
  - "toggle10"
  - "toggle11"
  - "toggle12"
  - "toggle13"
  - "toggle2"
  - "toggle3"
  - "toggle4"
  - "toggle5"
  - "toggle6"
  - "toggle7"
  - "toggle8"
  - "toggle9"
  - "triangle"
  - "weather"
