# EnvOS (planned)

A small operating system written in EnvoL: a minimal, dependable core, and a clean
desktop drawn with EnvoR and EnvoUI.

First steps:

- Boot on x86-64 under QEMU (UEFI): a console, memory management, interrupts and a timer.
- A framebuffer desktop, input, and one app.
- EnvoVM, the runtime EnvOS programs run on, grown from the VM behind `envo run`.

Work starts once the compiler's generated code is as fast as it needs to be. Progress is
on the [roadmap](https://github.com/orgs/envoscale/projects/3).
