# EnvIDE: the IDE

A code editor and IDE written in EnvoL, built on EnvoUI.

<p align="center"><img src="https://raw.githubusercontent.com/envoscale/.github/main/profile/assets/envide.png" alt="EnvIDE with the EnvoLang repository in the sidebar and examples/02-shapes/main.envol open" width="100%"></p>

Today: a sidebar with the folder's files, tabs, the editor with syntax colors, a status
bar, and a command palette (Ctrl+Shift+P). Next: saving, then errors, completion and
go-to-definition from `envo lsp`, then build, run, test and debug.

```bash
git clone https://github.com/envoscale/EnvIDE
cd EnvIDE
./build.sh run                       # builds EnvoL once, then EnvIDE, and opens it
build/envide <folder> [file]         # open a folder, and a file in it
build/envide . main.envol --screenshot shot.ppm   # draw one frame into an image
```
