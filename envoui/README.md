# EnvoUI: the UI framework

One tree of components, laid out and drawn in a window, a browser page or a terminal.
Buttons and text, lists and trees that stay fast with thousands of rows, tabs, split
panes, a code editor with multiple cursors and undo, and a command palette. Every
component can be used with the keyboard alone, and both themes meet WCAG AA contrast.

<p align="center"><img src="https://raw.githubusercontent.com/envoscale/.github/main/profile/assets/ui-themes.png" alt="A settings card drawn by EnvoUI in the light and dark themes" width="100%"></p>

```cs
use envoui as ui;

ui.Tree t = ui.Tree.New();
u32 card = t.Card(t.Root());
t.Text(card, "Settings", ui.TITLE);
u32 dark = t.Checkbox(card, "Dark mode", false);
u32 save = t.Button(card, "Save", true);
```

The same tree is drawn with EnvoR in a window (`LayoutPixels`, `DrawPixels`) or in a
terminal (`LayoutCells`, `DrawCells`). Input arrives as events, so apps and their tests
drive a UI the same way.

| Module | |
|---|---|
| [`envoui`](https://github.com/envoscale/EnvoUI/tree/main/ui) | Components, layout, input, focus, drawing |
| [`envoui.edit`](https://github.com/envoscale/EnvoUI/tree/main/edit) | Text buffers: cursors, selections, undo, search |
| [`envoui.term`](https://github.com/envoscale/EnvoUI/tree/main/term) | Terminals: screens, styles, keys |

```
dependencies {
    envoui = { git = "https://github.com/envoscale/EnvoUI", rev = "<commit>" }
}
```
