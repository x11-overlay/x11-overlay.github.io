<div markdown="1" class="examples">
# Examples

## Ansi Color Example

To colorize a text line or just a single word the well known ansi escape codes can be used like it's common for text in a terminal.

For example selecting red as a foreground font color can be achieved by using one of three different ansi color codes:

- <span class="sgr">[91</span> selects "Bright Red" out of a 16 color palette (4bit)
- <span class="sgr">[38;5;9</span> selects "Intense Red" out of a 256 color palette (8bit)
- <span class="sgr">[38;2;255;0;0</span> use "Red" color from RGB colors (24bit)

![example console command](/assets/images/example_color_console_echo.webp)

By using multiple sequences in a single line, something more advanded can be achieved. Using
"<span class="sgr">[91</span>CRIT<span class="sgr">[38;5;248</span>: Disk Space Usage (<span class="sgr">[97</span>96%<span class="sgr">[38;5;248</span>)<span class="sgr">[0</span>" for instance can be used to generate a critical alarm message with some details. The provided example file in the docs folder results to:
![example console command](/assets/images/example_color_console_cat.webp)

What you see in the console above is what you get with x11-overlay.

```
$> x11-overlay \
    docs/example-alarms.utf8.ans
```

![example console command](/assets/images/example_color_overlay.webp)

## Ansi Font Example

The default font can be specified using the <span class="option-param">-f</span> or <span class="option-param">\--font-name</span> option, and the default font size with the <span class="option-param">-s</span> or <span class="option-param">\--font-size</span> option.

In addition to the primary default font, alternative fonts can be selected dynamically by using ANSI control codes <span class="sgr">[11</span> to <span class="sgr">[19</span> within the text. To enable the use of alternative fonts or font sizes, their names or values must be provided as comma-separated lists in the respective option parameters.  
The control code <span class="sgr">[10</span> resets the font and font size to the primary defaults.

A command to enable multiple fonts and font sizes.

```
./bin/overlay -f NotoSansMono,JetBrainsMono -s 12,18 \
    docs/example-alarms.utf8.ans
```

As _NotoSansMono_ is the default font name and _12_ the default font size, they may be omitted in the parameter list by leaving the corresponding entry blank. This command produces the same result as the previous command, while omitting the explicit specification of the defaults - note the leading commata.

```
./bin/overlay -f ,JetBrainsMono -s ,18 \
    docs/example-alarms.utf8.ans
```

![example console command](/assets/images/example_font_overlay.webp)

</div>

## Config File Example

Instead of passing all arguments in the command line, they can be provided by specifing a config file. Config files use the INI format. For the previous ANSI color example a config file _example-alarms.ini_ leads to the same result when the content is the following:

```txt
InputFile=docs/example-alarms.utf8.ans

[Positioning]
Orientation=SW

[Font]
Name=NotoSansMono,JetBrainsMono
Size=12,18
```

```
./bin/overlay -c example-alarms.ini
```
