# A tour of EnvoL

EnvoL compiles to small native programs for Windows, Linux, macOS and the browser, and
runs the same code as a sandboxed script. Memory is managed by ownership: no garbage
collector, and no manual freeing. Every snippet here runs as shown.

## Values and functions

```cs
use alloc.text;

i64 Square(i64 x) => x * x;

print(text.Int(Square(7)).AsStr());     // 49
```

Types come first, as in `i64 x`. A function whose body is one expression can use `=>`.
Integers are `i8` to `i64` and `u8` to `u64`, plus `usize`; arithmetic that overflows
stops the program instead of wrapping silently.

## Structs and methods

```cs
struct Point {
    i64 X;
    i64 Y;

    public i64 Dist2(in this) => this.X * this.X + this.Y * this.Y;
}

void Grow(ref Point p, i64 by) {
    p.X += by;
    p.Y += by;
}

Point p = new Point { X = 3, Y = 4 };
Grow(ref p, 1);
print(text.Int(p.Dist2()).AsStr());     // 41
```

A parameter says how it uses its argument:

| | |
|---|---|
| `T x` | takes the value (moves it, or copies a small one) |
| `in T x` | reads it |
| `ref T x` | changes it; the caller writes `ref` too, so changes are visible at the call |
| `out T x` | fills it in |

## Enums and `match`

```cs
enum Shape {
    Circle(i64 radius),
    Rect(i64 width, i64 height),
}

i64 Area(in Shape s) => match s {
    Circle(r) => 3 * r * r,
    Rect(w, h) => w * h,
};
```

`match` must cover every case, so adding a variant shows you every place to update.

## Optional values

```cs
i64? FirstEven(in List<i64> xs) {
    foreach (var x in xs.AsSlice()) {
        if (x % 2 == 0) return Some(x);
    }
    return null;
}

List<i64> xs = List<i64>.New();
xs.Push(3);
xs.Push(8);
print(text.Int(FirstEven(xs) ?? -1).AsStr());     // 8
```

`T?` is a value that may be missing. `??` gives a fallback. Operations that can fail
return a `Result`, which holds either the value or the error.

## Collections

```cs
use alloc.map.{Map};

Map<str, i64> ages = Map<str, i64>.New();
ages.Set("ada", 36);
print(text.Int(ages.GetOr("ada", 0)).AsStr());     // 36
```

`List<T>`, `Map<K, V>` and `string` own their contents and free them when they go out of
scope. `str` is a borrowed view of text.

## Interfaces and generics

```cs
interface IShape {
    i64 Area(in this);
}

struct Square : IShape {
    i64 Side;
    public i64 Area(in this) => this.Side * this.Side;
}

i64 Twice<T>(in T shape) where T : IShape => 2 * shape.Area();
```

A generic function is compiled once for each type it is used with, so calls through an
interface cost nothing extra.

## Files, and the sandbox

```cs
use std.fs;

var read = fs.ReadText("notes.txt");
if (read.IsErr()) {
    print("cannot read notes.txt");
    return 1;
}
print(read.Unwrap().AsStr());
```

Run as a script, this needs permission: `envo --allow read notes.envol`. Built as a
native program, it runs with the permissions of whoever starts it.

## Where next

- [The examples](https://github.com/envoscale/EnvoLang/tree/main/examples): JSON,
  cryptography, generics and more.
- [The specification](https://github.com/envoscale/EnvoLang/tree/main/spec): every rule,
  with examples.
- [The standard library](https://github.com/envoscale/EnvoLang/tree/main/lib): `core`,
  `alloc`, `std`, and `envo.*` for crypto, TLS, HTTP, JSON and AI.
