# vim - Vi IMproved

vim is a clone of Bill Joy's *vi text editor* program for Unix. It was written
by Bram Moolenaar based on source for a port of the Stevie editor to the Amiga
and first released publicly in 1991.
Vim is free and open source software and is released under a license that
includes some charityware clauses, encouraging users who enjoy the software
to consider donating to children in Uganda.

Vim's interface is not based on menus or icons but on commands given in
a text user interface;
its GUI mode, **gVim**, adds menus and toolbars for commonly used commands
but the full functionality is still expressed through its command line mode.
Vi (and by extension Vim) tends to allow a typist to keep their fingers on the home row.


Vim has a built-in tutorial for beginners (`vimtutor` command).
Vim also has a built-in help facility (`:help` command) that allows users to query
and navigate through commands and features.


## Modes in vim

- **normal**
- **insert**
- **visual**

**Simple easy to use commands** - *Say them in your head & you get it right!*

### NORMAL mode (<kbd>Esc</kbd>)

- <kbd>H</kbd> Left
- <kbd>J</kbd> Down
- <kbd>K</kbd> Up
- <kbd>L</kbd> Right
- <kbd>i</kbd> Insert Mode
- <kbd>A</kbd> Insert Mode at end of current line
- <kbd>x</kbd> Delete current Character
- <kbd>X</kbd> Delete character to the left(<kbd>backspace</kbd>)
- <kbd>u</kbd> undo last action
- <kbd>ctrl</kbd> + <kbd>R</kbd> redo last action
- <kbd>0</kbd> Jump to beginning of line
- <kbd>$</kbd> Jump to end of line
- <kbd>w</kbd> Jump to next word(alphanumberic or punctuations)
- <kbd>b</kbd> Jump to prev word(alphanumberic or punctuations)
- <kbd>e</kbd> Jump to end word(alphanumberic or punctuations)
- <kbd>W</kbd> Jump to next word(sequence of non-blank characters)
- <kbd>B</kbd> Jump to prev word(sequence of non-blank characters)
- <kbd>E</kbd> Jump to end word(sequence of non-blank characters)
- <kbd>R</kbd> Insert Mode with overstrike cursor, which types over existing characters
- <kbd>:</kbd><kbd>w</kbd> Save
- <kbd>:</kbd><kbd>q</kbd> Quit


**C** - Change
**D** - Delete
**I** - Inside
**"** - Quotes
**)** - Parens

![Git Cheetsheet](http://www.viemu.com/vi-vim-cheat-sheet.gif)

Source: http://www.viemu.com
