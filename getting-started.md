# Getting started

## Install

Download the archive for your system from the
[releases](https://github.com/envoscale/EnvoLang/releases), unpack it, and put its `bin`
folder on your `PATH`. Check it works:

```bash
envo version
```

Or build from source. You need only Git and a shell (Git Bash on Windows works, or
PowerShell with `build.ps1`):

```bash
git clone https://github.com/envoscale/EnvoLang
cd EnvoLang
./build.sh build            # build/envo/envo, about a minute
```

## Your first program

Save this as `hello.envol`:

```cs
print("Hello, World!");
```

Run it:

```bash
envo hello.envol
```

One line is a whole program. There is no `main` to write: the statements at the top of a
file run in order.

## Scripts and native programs

`envo hello.envol` runs the file as a script, in a sandbox. A script cannot read files,
write files, use the network or start programs unless you allow it:

```bash
envo --allow read notes.envol        # may read files
envo --allow read:data notes.envol   # may read files under data/ only
```

If a script tries something it was not allowed, `envo` stops it and says which
permission it needs.

`envo build` makes a native executable instead. It is small, starts instantly and needs
nothing installed to run. Any target can be built from any system:

```bash
envo build hello.envol -o hello
envo build hello.envol -o hello.exe --target x86_64-windows
```

Targets: `x86_64-windows`, `x86_64-linux`, `aarch64-linux`, `aarch64-macos` and
`wasm32-web`.

## Your first package

A package is a folder with an `envo.envon` manifest:

```bash
envo new greeter
cd greeter
envo run .          # prints Hello, greeter!
envo test           # runs tests/
```

`envo new` creates `main.envol` (the program), `greet.envol` (code the program and tests
share) and `tests/greet.envol`. Every `.envol` file outside `tests/` is part of the
package.

A test is a program whose expected output is written at its top:

```cs
// expect: Hello, test!
print(Greeting("test").AsStr());
```

## Using other packages

List them in `envo.envon`:

```
dependencies {
    envor = { git = "https://github.com/envoscale/EnvoR", rev = "<commit>" }
    mylib = { path = "../mylib" }
}
```

A git dependency is pinned to a full commit, so a build today and a build next year use
the same code. Then `use` its modules:

```cs
use envor.gfx;
```

## Editors

`envo lsp` gives any editor that speaks the Language Server Protocol errors as you type.
For VS Code there is an extension in
[`adapters/editors/vscode`](https://github.com/envoscale/EnvoLang/tree/main/adapters/editors/vscode).
[EnvIDE](envide/README.md) is the IDE written in EnvoL.

## When something goes wrong

Every error has a code. `envo explain` tells you what it means and the rule behind it:

```bash
envo explain E0301
```

## Next

- [A tour of EnvoL](envol/README.md)
- [The examples](https://github.com/envoscale/EnvoLang/tree/main/examples)
- [Every `envo` command](envopm/README.md#commands)
