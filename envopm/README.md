# EnvoPM: the `envo` tool

One program builds, runs, tests, formats, debugs and packages EnvoL code. It comes with
every [release](https://github.com/envoscale/EnvoLang/releases).

## Packages

A package is a folder with an `envo.envon` manifest. Every `.envol` file in it, outside
`tests/` and `build/`, is part of the package. `main.envol`, if there is one, is the
program.

```
#eon 1
package {
    name    = "greeter"
    version = "0.1.0"
    edition = "2027"
}
dependencies {
    envor = { git = "https://github.com/envoscale/EnvoR", rev = "<40-character commit>" }
    mylib = { path = "../mylib" }
    json  = "1.2.0"
}
```

| Dependency | |
|---|---|
| `{ path = "..." }` | A package in another folder |
| `{ git = "...", rev = "..." }` | A package in a git repository, at one commit |
| `"1.2.0"` | A package from a registry, fetched with `envo fetch` into `envo.lock.envon` |

Registry packages are signed archives: `envo publish` signs them with your key, and
`envo fetch` refuses an archive whose signature or checksum does not match.

## Commands

| Command | |
|---|---|
| `envo <file.envol>` | Run a script in the sandbox (`--allow read,write,net,...`) |
| `envo new <name>` | Create a package |
| `envo run [dir]` | Run a package in the sandbox; `--native` builds and runs native code |
| `envo build [dir]` | Build a native program: `-O2`, `-o <file>`, `--target <t>`, `--sbom` |
| `envo test [path]` | Build and run every test, comparing output with its `expect:` lines |
| `envo check [dir]` | Check names, types and ownership without building |
| `envo fmt [path]` | Lay out code in the standard format; `--check` for CI |
| `envo dbg [dir]` | Debug: breakpoints, stepping, the call stack and locals |
| `envo prof [dir]` | Count calls and instructions per function |
| `envo fuzz <target>` | Coverage-guided fuzzing |
| `envo lsp` | Language server for editors |
| `envo explain <code>` | Explain an error code |
| `envo fetch`, `pack`, `publish` | Resolve, package and publish packages |
| `envo key`, `sign`, `verify` | Ed25519 keys and signatures |
| `envo archive` | A reproducible tar archive (used for releases) |

`envo help` prints the full list with every option.

## Permissions

Scripts start with no access to files, the network, the environment or other programs.
Each `--allow` grants one:

| | |
|---|---|
| `read`, `write`, `fs` | Files; add `:path` to limit them to a folder (`read:data`) |
| `env` | Environment variables |
| `run` | Starting other programs |
| `net` | The network |
| `all` or `-A` | Everything |
