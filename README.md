## FontForge Font Stripper ##

### Introduction ###

This small project provides some scripts to strip unnecessary glyphs from fonts to reduce their size. It's probably useful when you need to use some big fonts with your scripts but do not want to bloat the total size too much, like 100 kB ASS subtitle and 10 mB of fonts. 

This is the first thing I write with Python, and it just happens to work. If something goes wrong, don't hesitate to bug me.

### Requirements ###

- [FontForge][fontforge]
- Python (either 2 or 3)
- A terminal

### Usage ###

This ultilizes FontForge, the powerful yet free font editor, to maniputate fonts via a script written in FontForge's own (legacy) language. I've generated some scripts for stripping everything but some certain sets of characters. If they suit your need, just use them. If you need something more specific, just generate your own script; it's quite easy.

#### Pre-made scripts ####

- ascii_chars.pe: This script can be used to strip everything but printable ASCII characters. Everything means everything; only ASCII characters will be retained. See ascii_chars_list.txt for the full list.

- basic_latin_chars.pe: This script can be used to strip everything but characters in Adobe Glyph List For New Fonts v1.7, Windows Glyph List 4, and Vietnamese characters. It should covers most characters in most latin-based languages and some common symbols; of course, all ASCII characters are included. See basic_latin_chars.txt for the full list.

- basic_latin_chars_w_symbols.pe: This script can be used to strip everything but characters in Adobe Glyph List For New Fonts v1.7, Windows Glyph List 4, Vietnamese characters, and some more punctuation marks and typographic symbols. Everything in basic_latin_chars are included. See basic_latin_chars_w_symbols.txt for the full list.

#### Generating scripts ####

This is what you need Python for. 

Open terminal, type the command like this:

`python font_stripping_script_generator.py output_script.pe input_text_1.txt [input_text_2.txt input_text_3.txt ...]`

Input text file should be plain text, encoded in UTF-8. You can add as many input files as you want. 

ASS subtitles are usually already encoded in UTF-8, so just throw it there.

For example:

`python font_stripping_script_generator.py test3.pe "basic_latin_chars_w_symbols_list.txt" "[FFF] Unbreakable Machine-Doll - 01 [8625CBFC]_Track02.ass"`

#### Stripping fonts ####

When you have all necessary files and programs, open terminal, and then type the command like this:

`fontforge -script basic_latin_chars.be input_original_font.ttf output_stripped_font.ttf`

Replace fontforge with path to FontForge executable, which is typically `C:\Program Files (x86)\FontForge\run_fontforge.exe` or `C:\Program Files\FontForge\run_fontforge.exe` in Windows; `/usr/local/bin/fontforge`, `/usr/bin/fontforge`, or simply `fontforge` in Linux/Unix.

Replace basic_latin_chars.be with the script you want to use.

For example:

`"C:\Program Files (x86)\FontForge\run_fontforge.exe" -script "F:\Typography\tools\Strip font\basic_latin_chars.pe" "F:\Typography\tools\Strip font\Arial_Unicode_MS.TTF" "F:\Typography\tools\Strip font\Arial_Unicode_MS_naked.TTF"`

`fontforge -script ~/Desktop/basic_latin_chars.pe ~/Desktop/Arial_Unicode_MS.TTF ~/Desktop/Arial_Unicode_MS_nake.TTF`

### Inportant note ###

For the love of typography, in case you want to distribute a stripped font, please consider renaming it to something else like OriginalName-latinonly, and naming the file somewhat differently from its original name. You don't want someone to get haunted with some incomplete fonts for life, right?

### Acknowledgements ###

This project is inspired and influented heavily by [Font Forge Glyph Stripper][fontstripper] (Huan Truong) and [Strip unused glyphs][Strip_unused_glyphs] (Koichi Akabe). Thanks to them, my life is easier.

[fontforge]: http://sourceforge.net/projects/fontforge/
[fontstripper]: https://gist.github.com/htruong/1596735
[Strip_unused_glyphs]: http://www.renpy.org/wiki/renpy/doc/cookbook/Reduce_the_size_of_a_font_file