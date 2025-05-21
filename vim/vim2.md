# Vim Editor Cheatsheet

A comprehensive guide to navigating and using the Vim text editor efficiently.

## Table of Contents
- [Modes](#modes)
- [Basic Navigation](#basic-navigation)
- [Editing Text](#editing-text)
- [Search and Replace](#search-and-replace)
- [Working with Files](#working-with-files)
- [Visual Mode](#visual-mode)
- [Multiple Windows](#multiple-windows)
- [Macros](#macros)
- [Text Objects](#text-objects)
- [Miscellaneous Tips](#miscellaneous-tips)

## Modes

### Normal Mode
- Default mode when opening Vim
- Used for navigation and entering commands

### Insert Mode
- `i` - Insert before cursor
- `I` - Insert at beginning of line
- `a` - Append after cursor
- `A` - Append at end of line
- `o` - Open new line below
- `O` - Open new line above
- `Esc` or `Ctrl+[` - Return to Normal mode

### Visual Mode
- `v` - Character-wise visual mode
- `V` - Line-wise visual mode
- `Ctrl+v` - Block-wise visual mode

### Command Mode
- `:` - Enter command mode

## Basic Navigation

### Moving the Cursor
- `h` - Move left
- `j` - Move down
- `k` - Move up
- `l` - Move right

### Word Navigation
- `w` - Move to start of next word
- `e` - Move to end of current/next word
- `b` - Move to beginning of current/previous word

### Line Navigation
- `0` - Move to start of line
- `$` - Move to end of line
- `^` - Move to first non-blank character

### Document Navigation
- `gg` - Go to first line
- `G` - Go to last line
- `:n` - Go to line number n
- `nG` - Go to line number n

### Screen Navigation
- `Ctrl+f` - Page down
- `Ctrl+b` - Page up
- `Ctrl+d` - Half page down
- `Ctrl+u` - Half page up
- `zz` - Center cursor on screen
- `zt` - Position cursor at top of screen
- `zb` - Position cursor at bottom of screen

## Editing Text

### Delete Operations
- `x` - Delete character under cursor
- `X` - Delete character before cursor
- `dw` - Delete word
- `d$` or `D` - Delete to end of line
- `dd` - Delete entire line
- `ndd` - Delete n lines

### Change Operations
- `r` - Replace one character
- `cw` - Change word
- `c$` or `C` - Change to end of line
- `cc` - Change entire line

### Copy and Paste
- `y` - Yank (copy) selected text
- `yy` - Yank entire line
- `nyy` - Yank n lines
- `p` - Paste after cursor
- `P` - Paste before cursor

### Undo/Redo
- `u` - Undo last change
- `Ctrl+r` - Redo

## Search and Replace

### Search
- `/pattern` - Search forward for pattern
- `?pattern` - Search backward for pattern
- `n` - Next match in same direction
- `N` - Next match in opposite direction
- `*` - Search forward for word under cursor
- `#` - Search backward for word under cursor

### Replace
- `:%s/old/new/g` - Replace all occurrences of "old" with "new"
- `:%s/old/new/gc` - Replace with confirmation
- `:s/old/new/g` - Replace in current line only

## Working with Files

### Opening/Saving Files
- `:e filename` - Open file
- `:w` - Save current file
- `:w filename` - Save as
- `:wq` or `:x` or `ZZ` - Save and quit
- `:q` - Quit
- `:q!` or `ZQ` - Quit without saving

### Multiple Files
- `:bn` - Next buffer
- `:bp` - Previous buffer
- `:bd` - Delete buffer
- `:ls` - List buffers

## Visual Mode

### Selection
- `v` + motion - Select text
- `V` + motion - Select lines
- `Ctrl+v` + motion - Select block

### Operations with Selection
- `d` - Delete selection
- `y` - Yank selection
- `c` - Change selection
- `>` - Indent selection
- `<` - Outdent selection
- `=` - Auto-indent selection

## Multiple Windows

### Window Management
- `:split` or `:sp` - Horizontal split
- `:vsplit` or `:vs` - Vertical split
- `Ctrl+w s` - Horizontal split
- `Ctrl+w v` - Vertical split
- `Ctrl+w c` - Close window
- `Ctrl+w o` - Close all windows except current

### Window Navigation
- `Ctrl+w h` - Move to left window
- `Ctrl+w j` - Move to window below
- `Ctrl+w k` - Move to window above
- `Ctrl+w l` - Move to right window
- `Ctrl+w w` - Cycle through windows

## Macros

### Recording Macros
- `qa` - Start recording macro into register a
- `q` - Stop recording
- `@a` - Execute macro a
- `@@` - Repeat last executed macro
- `5@a` - Execute macro a 5 times

## Text Objects

### Selection with Text Objects
- `iw` - Inner word
- `aw` - A word (includes surrounding space)
- `is` - Inner sentence
- `as` - A sentence
- `ip` - Inner paragraph
- `ap` - A paragraph
- `i"` - Inner quotes
- `a"` - A quotes (includes quotes)
- `i(` or `i)` - Inner parentheses
- `a(` or `a)` - A parentheses (includes parentheses)

### Combining Operations with Text Objects
- `ciw` - Change inner word
- `dap` - Delete a paragraph
- `yi"` - Yank text inside quotes

## Miscellaneous Tips

### Marks
- `ma` - Set mark a at current position
- `'a` - Jump to line of mark a
- `` `a `` - Jump to position of mark a

### Folding
- `zf` - Create fold
- `zo` - Open fold
- `zc` - Close fold
- `zR` - Open all folds
- `zM` - Close all folds

### Various
- `.` - Repeat last change
- `Ctrl+g` - Show file status
- `:set nu` - Show line numbers
- `:set nonu` - Hide line numbers
- `:help keyword` - Open help for keyword

---

*This cheatsheet covers the basics of Vim. For more detailed information, use `:help` within Vim or visit [Vim's official documentation](https://www.vim.org/docs.php).*
