# Vim Shortcuts Reference Guide

## Introduction

Vim is a powerful text editor available on most Linux systems. Known for its efficiency, Vim allows users to perform complex editing tasks with minimal keystrokes. This README provides a comprehensive reference of essential Vim shortcuts to help boost your productivity.

## Getting Started

### Opening and Closing Files

| Command | Description |
|---------|-------------|
| `vim filename` | Open a file in Vim |
| `:w` | Save changes |
| `:q` | Quit Vim (fails if there are unsaved changes) |
| `:wq` or `ZZ` | Save and quit |
| `:q!` or `ZQ` | Quit without saving changes |
| `:w filename` | Save as a new file |

## Vim Modes

Vim operates in several modes:

1. **Normal Mode**: Default mode for navigation and commands
2. **Insert Mode**: For inserting and editing text
3. **Visual Mode**: For selecting text
4. **Command-Line Mode**: For executing commands

### Switching Between Modes

| Command | Description |
|---------|-------------|
| `Esc` | Return to Normal mode from any other mode |
| `i` | Enter Insert mode before cursor |
| `I` | Enter Insert mode at beginning of line |
| `a` | Enter Insert mode after cursor |
| `A` | Enter Insert mode at end of line |
| `v` | Enter Visual mode |
| `V` | Enter Visual Line mode |
| `Ctrl+v` | Enter Visual Block mode |
| `:` | Enter Command-line mode |

## Navigation (Normal Mode)

### Basic Movement

| Command | Description |
|---------|-------------|
| `h` | Move cursor left |
| `j` | Move cursor down |
| `k` | Move cursor up |
| `l` | Move cursor right |
| `w` | Move to start of next word |
| `b` | Move to start of previous word |
| `e` | Move to end of word |
| `0` | Move to start of line |
| `^` | Move to first non-blank character of line |
| `$` | Move to end of line |

### Advanced Movement

| Command | Description |
|---------|-------------|
| `gg` | Go to first line of document |
| `G` | Go to last line of document |
| `nG` | Go to line n |
| `:n` | Go to line n |
| `Ctrl+f` | Page down |
| `Ctrl+b` | Page up |
| `%` | Jump to matching bracket |
| `*` | Search forward for word under cursor |
| `#` | Search backward for word under cursor |
| `{` | Jump to previous paragraph |
| `}` | Jump to next paragraph |

## Editing Text

### Inserting Text

| Command | Description |
|---------|-------------|
| `i` | Insert before cursor |
| `I` | Insert at beginning of line |
| `a` | Append after cursor |
| `A` | Append at end of line |
| `o` | Open new line below current line |
| `O` | Open new line above current line |

### Deleting Text

| Command | Description |
|---------|-------------|
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |
| `dd` | Delete current line |
| `dw` | Delete from cursor to end of word |
| `d$` or `D` | Delete from cursor to end of line |
| `d0` | Delete from cursor to beginning of line |
| `dgg` | Delete from cursor to beginning of file |
| `dG` | Delete from cursor to end of file |
| `ndd` | Delete n lines |

### Changing Text

| Command | Description |
|---------|-------------|
| `r` | Replace single character |
| `R` | Enter Replace mode |
| `cw` | Change word |
| `cc` | Change entire line |
| `C` | Change from cursor to end of line |
| `~` | Switch case of character under cursor |
| `u` | Undo last change |
| `Ctrl+r` | Redo last undone change |

### Copy and Paste

| Command | Description |
|---------|-------------|
| `yy` | Yank (copy) current line |
| `yw` | Yank word |
| `y$` | Yank to end of line |
| `p` | Paste after cursor |
| `P` | Paste before cursor |

## Searching and Replacing

| Command | Description |
|---------|-------------|
| `/pattern` | Search forward for pattern |
| `?pattern` | Search backward for pattern |
| `n` | Repeat search in same direction |
| `N` | Repeat search in opposite direction |
| `:%s/old/new/g` | Replace all occurrences of 'old' with 'new' |
| `:%s/old/new/gc` | Replace all occurrences with confirmation |

## Working with Multiple Files

| Command | Description |
|---------|-------------|
| `:e filename` | Edit a file |
| `:sp filename` | Open file in horizontal split |
| `:vsp filename` | Open file in vertical split |
| `Ctrl+ws` | Split window horizontally |
| `Ctrl+wv` | Split window vertically |
| `Ctrl+ww` | Switch between windows |
| `Ctrl+wq` | Quit current window |
| `:buffers` | List all buffers |
| `:bn` | Go to next buffer |
| `:bp` | Go to previous buffer |
| `:bd` | Delete buffer |

## Visual Mode

| Command | Description |
|---------|-------------|
| `v` | Start visual mode |
| `V` | Start linewise visual mode |
| `Ctrl+v` | Start visual block mode |
| `d` | Delete selected text |
| `y` | Yank (copy) selected text |
| `>` | Indent selected text |
| `<` | Unindent selected text |

## Text Objects (use with d, y, c, etc.)

| Command | Description |
|---------|-------------|
| `iw` | Inner word |
| `aw` | A word (includes surrounding space) |
| `is` | Inner sentence |
| `as` | A sentence |
| `ip` | Inner paragraph |
| `ap` | A paragraph |
| `i(` or `i)` | Inside parentheses |
| `a(` or `a)` | Around parentheses |
| `i"` | Inside double quotes |
| `a"` | Around double quotes |

## Marks

| Command | Description |
|---------|-------------|
| `ma` | Set mark 'a' at current position |
| `'a` | Jump to line of mark 'a' |
| `` `a `` | Jump to position of mark 'a' |
| `:marks` | List all marks |

## Macros

| Command | Description |
|---------|-------------|
| `qa` | Record macro 'a' |
| `q` | Stop recording macro |
| `@a` | Execute macro 'a' |
| `@@` | Repeat last executed macro |

## Folding

| Command | Description |
|---------|-------------|
| `zf` | Create fold |
| `zo` | Open fold |
| `zc` | Close fold |
| `za` | Toggle fold |
| `zR` | Open all folds |
| `zM` | Close all folds |

## Configuration

- Your Vim configuration is stored in `~/.vimrc`
- To make Vim more user-friendly, consider adding these lines to your `.vimrc`:

```vim
set number          " Show line numbers
syntax on           " Enable syntax highlighting
set autoindent      " Auto indent
set tabstop=4       " Tab width is 4 spaces
set shiftwidth=4    " Indent width is 4 spaces
set smarttab        " Use smart tabs
set mouse=a         " Enable mouse support
set incsearch       " Incremental search
set hlsearch        " Highlight search results
```

## Getting Help

| Command | Description |
|---------|-------------|
| `:help` | Open help |
| `:help command` | Get help for specific command |
| `:q` | Close help window |

## Tips for Beginners

1. Learn incrementally - don't try to memorize all commands at once
2. Practice navigation commands (h, j, k, l) until they become second nature
3. Use `vimtutor` (terminal command) for interactive learning
4. Keep a cheat sheet handy while learning
5. Focus on efficiency - what tasks do you perform frequently?

## Additional Resources

- `vimtutor` - Interactive Vim tutorial (run from terminal)
- [Vim official website](https://www.vim.org/)
- [Vim Tips Wiki](https://vim.fandom.com/wiki/Vim_Tips_Wiki)
- [Vim Adventures](https://vim-adventures.com/) - Game to learn Vim

Happy editing with Vim!
