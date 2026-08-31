# Vim Text Editor Reference

## Modes
- **Normal Mode**: Default mode for navigation and manipulation.
- **Insert Mode**: For entering text.
- **Command-line Mode**: For saving, quitting, and complex commands.

## 1. Navigation (Normal Mode)
Efficiently moving through large configuration files.

| Command | Description |
| :--- | :--- |
| `h` / `l` | Move left / right |
| `j` / `k` | Move down / up |
| `w` | Jump to the start of the next word |
| `e` | Jump to the end of the current word |
| `b` | Jump to the start of the previous word |
| `0` (zero) | Jump to the beginning of the current line |
| `^` | Jump to the first non-blank character of the line |
| `$` | Jump to the end of the current line |
| `gg` | Go to the first line of the file |
| `G` | Go to the last line of the file |
| `Ctrl + f` | Page Down |
| `Ctrl + b` | Page Up |
| `Ctrl + d` | Half-page Down |
| `Ctrl + u` | Half-page Up |
| `Ctrl + e` | Scroll line down |
| `Ctrl + y` | Scroll line up |

## 2. Editing & Manipulation (Normal Mode)
Modifying text and managing lines.

| Command | Description |
| :--- | :--- |
| `i` | Enter Insert mode at the cursor position |
| `a` | Append (Insert after the cursor) |
| `I` (Shift+i) | Insert at the beginning of the current line |
| `o` | Open a new line below the current line |
| `O` (Shift+o) | Open a new line above the current line |
| `x` | Delete a single character under the cursor |
| `dd` | Delete (cut) the current line |
| `D` | Delete from cursor to the end of the line |
| `dG` | Delete from current position to the end of the file |
| `yy` | Yank (copy) the current line |
| `p` | Paste the yanked text after the cursor |
| `u` | Undo last action |
| `Ctrl + r` | Redo last undone action |

## 3. Search & Save (Command-line Mode)
Finding patterns and persisting changes.

| Command | Description |
| :--- | :--- |
| `/pattern` | Search forward for a specific pattern |
| `:w [filename]` | Save as (Write to a new filename) |
| `:w` | Save the current file |
| `:q` | Quit Vim |
| `:wq` | Save and quit |
| `:q!` | Quit without saving changes |


