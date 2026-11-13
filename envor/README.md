# EnvoR: rendering

2D drawing, TrueType fonts, 3D with physically based shading, the math under them, an
entity store, and the themes every EnvoUI app is drawn with. Everything is computed in
EnvoL on the CPU, so a picture comes out the same on every platform.

<p align="center"><img src="https://raw.githubusercontent.com/envoscale/.github/main/profile/assets/render3d.png" alt="A blue cube between a gold metal sphere and a red plastic sphere, rendered by envor.render3d" width="100%"></p>

```cs
use envor.gfx;

gfx.Canvas c = gfx.Canvas.New(64, 48);
c.Clear(gfx.Color.Hex("#f5f5f7"));
c.FillRoundedRect(4, 4, 56, 40, 10, gfx.Color.Hex("#ffffff"));
c.FillCircle(18, 24, 8, gfx.Color.Hex("#0a64d4"));
```

| Module | |
|---|---|
| [`envor.gfx`](https://github.com/envoscale/EnvoR/tree/main/gfx) | Canvases: anti-aliased shapes, blending, clipping, images |
| [`envor.font`](https://github.com/envoscale/EnvoR/tree/main/font) | TrueType fonts: parsing, rasterizing, text layout |
| [`envor.render3d`](https://github.com/envoscale/EnvoR/tree/main/render3d) | Meshes, cameras, lights, materials, glTF 2.0 import |
| [`envor.math`](https://github.com/envoscale/EnvoR/tree/main/math) | Vectors, matrices, quaternions |
| [`envor.ecs`](https://github.com/envoscale/EnvoR/tree/main/ecs) | Entities and components |
| [`envor.theme`](https://github.com/envoscale/EnvoR/tree/main/theme) | Colors, type, spacing and shapes, light and dark ([design](theme-design.md)) |

Add it to a package:

```
dependencies {
    envor = { git = "https://github.com/envoscale/EnvoR", rev = "<commit>" }
}
```
