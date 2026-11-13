# EnvIDE roadmap

What an editor needs before it beats opening a file in Notepad, then what makes it an IDE.
Each stage is usable on its own; nothing ships without tests, a stress run and use in a
real window.

## 1. A real editor

In EnvIDE 0.3.0: the menu bar, files (without recent files), unsaved changes with
backups, tabs (without reordering), icons, Find and Replace, Go to Line, toggle comment,
auto-indent and zoom. Still to do: files changed outside, matching brackets, word wrap,
DPI scaling and settings.

| | |
|---|---|
| **Menu bar** | File, Edit, Selection, View, Go, Run, Terminal, Help, with every item's shortcut shown |
| **Files** | New, Open File, Open Folder, Save (Ctrl+S), Save As, Save All, Close, Revert; recent files and folders |
| **Unsaved changes** | A dot on the tab and in the title; asked before closing or quitting; never lost on a crash (a backup is kept until the file is saved) |
| **Tabs** | Many files open at once; Ctrl+Tab to switch; close, close others, reorder |
| **Files changed outside** | Reloaded when unchanged here, offered a choice when both changed |
| **Icons** | By language: the EnvoL mark for `.envol`, `.envon` and `.eir`, and icons for Markdown, JSON, images, text, folders |
| **Editing basics** | Find and replace (in a file), Go to Line, toggle comment, indent and outdent, auto-indent, matching brackets, word wrap, zoom (Ctrl+= and Ctrl+-) |
| **Screens** | Scaled for the display's DPI, so text is the same size on every screen |
| **Settings** | Theme, font size, tab width, line endings, keys: in a settings file, and on a page |

## 2. Layout

| | |
|---|---|
| **Panels** | Side bar, editor area and bottom panel, each dragged to any size, hidden and shown |
| **Split editors** | Two or more files side by side, or above and below |
| **Saved layout** | Per folder: open files, sizes and which panels show |
| **Bottom panel** | Problems, Output, Terminal |

## 3. Language features (from `envo lsp`)

| | |
|---|---|
| **Diagnostics** | Errors underlined as you type, listed in Problems |
| **Completion** | A menu at the cursor as you type; Tab or Enter accepts, Escape closes |
| **Navigation** | Go to Definition, Find References, symbols in the file, Quick Open (Ctrl+P) |
| **Hover and signatures** | A function's type and parameters |
| **Rename and format** | Rename a symbol everywhere; format with `envo fmt` |
| **Search** | Across the folder (Ctrl+Shift+F), with replace |

## 4. Build, run, debug

| | |
|---|---|
| **Tasks** | Build, Run, Test with `envo`; errors in Output are links to the place |
| **Terminal** | The system shell in the bottom panel |
| **Debugger** | Breakpoints, stepping, the call stack and variables, from `envo dbg` |
| **Git** | Changed files, gutter marks, diff, stage and commit |

## 5. Plugins

| | |
|---|---|
| **Plugins** | Programs that add commands, menu items, languages, themes and panels. Each runs as its own process and talks to EnvIDE over a small protocol, so a broken plugin cannot crash the editor |
| **Plugin manager** | Browse, install, update, turn on and off, remove; each plugin pinned to a commit, like EnvoPM packages |
| **EnvIDE Plugins** | A repository of first-party plugins and the plugin protocol's documentation |
