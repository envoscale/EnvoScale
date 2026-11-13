# RFC 0007: No `key { … }` shorthand in EnvoL initializers

- **Status:** Accepted (2026-11-12)
- **Author(s):** EnvoScale project
- **Affects:** language (initializers), EON (no change)
- **Tracking:** [#32](https://github.com/envoscale/EnvoLang/issues/32); closes the open question in `docs/spec/eon.md` section 4

## Summary

EON accepts both `server = { port = 8080 }` and the shorthand `server { port = 8080 }`.
EnvoL initializers accept only the first form: a nested initializer always follows `=`.
EON files keep the shorthand, and EON's canonical form keeps writing it. `[eon.envol.1]`
(an EON value is a valid EnvoL initializer) is restated for the form with `=`; pasting a
block written with the shorthand into EnvoL gets an error whose fix-it inserts the `=`.

## Motivation

`docs/spec/eon.md` section 4 left open whether EnvoL initializers take the shorthand. It
has to be settled before anonymous initializers (`Config c = { … };`) are implemented in
Stage 2, because the shorthand changes what the parser must accept inside braces.

## Guide-level explanation (the simple door)

In an EnvoL initializer, every field is `Name = value`, including nested ones:

```envo
Config c = {
    name = "api",
    server = { host = "0.0.0.0", port = 8080 },
};
```

In an `.envon` file you may also write the nested block without `=`, which reads well for
configuration:

```eon
server {
    host = "0.0.0.0"
    port = 8080
}
```

If you paste a block written that way into EnvoL code, the compiler says a nested
initializer needs `=`, and its fix-it adds it.

## Reference-level explanation (the full-control door)

- **[init.field.1]** (language) Inside an initializer, a field is `Ident '=' Expr`. The
  sequence `Ident '{'` inside an initializer is an error: **E0118** "a nested initializer
  needs `=`: write `name = { … }`", with a fix-it that inserts ` =`.
- **[eon.envol.1]** (EON, restated) An EON value whose nested blocks are written with `=`
  is a valid EnvoL initializer for its type. A value using the shorthand becomes one by
  inserting `=` before each nested `{`, which E0118's fix-it does.

Tests, when anonymous initializers land in Stage 2: an `s2-syntax` test for E0118 and its
fix-it. `envo.eon` is unchanged (its reader accepts both forms; its writer keeps the
shorthand).

## Drawbacks

Configuration written with the shorthand in `.envon` files needs `=` added before it can
be pasted into EnvoL; the fix-it does it.

## Alternatives

- **Accept the shorthand in EnvoL too.** Inside braces, `name { … }` would then be an
  initializer field, while elsewhere `name { … }` can begin a block after an expression
  statement or, later, a trailing lambda (`items.Each { … }`). Every brace after a name
  would need lookahead to tell which, in a position where a forgotten `=` or `;` already
  produces confusing errors. The gain is one character.
- **Remove the shorthand from EON.** Makes configuration files noisier, and the root
  `envo.envon` and Lumen's token files already use it.
- **Do nothing.** Leaves the question open and blocks anonymous initializers.


## Unresolved questions

None for the decision. E0118's number is provisional until the error registry assigns it.

## Migration / edition impact

None: EnvoL initializers never accepted the shorthand, and EON files do not change.
