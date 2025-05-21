Here's a concise and visually structured **GitHub README-style Vim Cheatsheet** for your repository:

---

# 🧠 Vim Cheat Sheet

Boost your productivity with this quick-reference guide to the **Vim code editor**. Perfect for beginners and intermediate users!

---

## 📦 Modes

| Mode        | Key   | Description                            |
| ----------- | ----- | -------------------------------------- |
| Normal      | `Esc` | Default mode for navigation & commands |
| Insert      | `i`   | Insert text before cursor              |
| Append      | `a`   | Insert text after cursor               |
| Visual      | `v`   | Select text                            |
| Line Visual | `V`   | Select full lines                      |
| Replace     | `R`   | Replace characters                     |
| Command     | `:`   | For commands like `:w`, `:q`           |

---

## 🧭 Navigation

| Action                      | Command            |
| --------------------------- | ------------------ |
| Move left/down/up/right     | `h`, `j`, `k`, `l` |
| Start/end of line           | `0`, `^`, `$`      |
| Forward/back word           | `w`, `b`           |
| Next/prev paragraph         | `{`, `}`           |
| Top/middle/bottom of screen | `H`, `M`, `L`      |
| Go to line `n`              | `:n`               |
| Go to matching bracket      | `%`                |

---

## ✍️ Insert Mode Shortcuts

| Action                    | Command  |
| ------------------------- | -------- |
| Insert before cursor      | `i`      |
| Insert at line start      | `I`      |
| Append after cursor       | `a`      |
| Append at line end        | `A`      |
| Open new line below/above | `o`, `O` |

---

## 🗂 File Commands

| Action              | Command       |
| ------------------- | ------------- |
| Save                | `:w`          |
| Quit                | `:q`          |
| Save and quit       | `:wq` or `ZZ` |
| Quit without saving | `:q!`         |
| Reload file         | `:e!`         |

---

## 🔁 Undo & Redo

| Action | Command    |
| ------ | ---------- |
| Undo   | `u`        |
| Redo   | `Ctrl + r` |

---

## ✂️ Copy, Cut & Paste

| Action             | Command   |
| ------------------ | --------- |
| Yank (copy) line   | `yy`      |
| Yank selection     | `y`       |
| Delete (cut) line  | `dd`      |
| Delete selection   | `d`       |
| Paste after/before | `p` / `P` |

---

## 🔍 Search & Replace

| Action                | Command         |
| --------------------- | --------------- |
| Search                | `/word`         |
| Search backward       | `?word`         |
| Next/previous match   | `n` / `N`       |
| Replace (one line)    | `:s/old/new/g`  |
| Replace (entire file) | `:%s/old/new/g` |

---

## 📐 Visual Mode

| Action                          | Command    |
| ------------------------------- | ---------- |
| Enter visual mode               | `v`        |
| Enter line visual               | `V`        |
| Select block (column)           | `Ctrl + v` |
| Yank/delete in visual           | `y`, `d`   |
| Indent                          | `>` / `<`  |
| Comment lines (plugin required) | `gc`       |

---

## 🧱 Indentation

| Action         | Command |
| -------------- | ------- |
| Indent line    | `>>`    |
| Un-indent line | `<<`    |
| Auto indent    | `=`     |

---

## 📑 Buffers, Tabs & Windows

| Action                | Command                            |
| --------------------- | ---------------------------------- |
| List buffers          | `:ls` or `:buffers`                |
| Switch buffer         | `:b <num>`                         |
| New tab               | `:tabnew`                          |
| Next/prev tab         | `:tabn`, `:tabp`                   |
| Split horizontally    | `:split` or `:sp`                  |
| Split vertically      | `:vsplit` or `:vsp`                |
| Switch between splits | `Ctrl + w` + direction (`h/j/k/l`) |

---

## ⚙️ Misc

| Action                 | Command                       |
| ---------------------- | ----------------------------- |
| Show line numbers      | `:set number`                 |
| Syntax highlighting    | `:syntax on`                  |
| Toggle paste mode      | `:set paste` / `:set nopaste` |
| Show current file path | `:echo expand("%:p")`         |

---

## 📌 Pro Tips

* Use `.` to repeat the last command.
* Use `:help <command>` to get help.
* Combine commands: `d3w` deletes 3 words, `y2j` yanks 2 lines down.


