# labelle-wgpu

The **wgpu** (WebGPU via [wgpu-native](https://github.com/gfx-rs/wgpu-native)) rendering backend for the [labelle](https://github.com/labelle-toolkit) 2D engine, as an **out-of-tree pluggable backend** (labelle-assembler#386).

Desktop-only (GLFW window + wgpu-native surface; Metal on macOS, Vulkan/DX elsewhere). Loop-style lifecycle.

## Use it

In a labelle project's `project.labelle`:

```zig
.backend = .wgpu,
.backend_package = .{ .name = "wgpu", .repo = "github.com/labelle-toolkit/labelle-wgpu", .version = "0.1.0" },
```

(Once `.backend = .wgpu` is flipped to resolve here by default, the `.backend_package` line is optional.)

## Layout

- `src/` — the four backend modules: `gfx`, `window`, `input`, `audio`
- `backend.manifest.zon` + `build_fragments/` — drive the assembler's manifest-splice codegen
- `templates/desktop.txt` — the generated `main()` run-loop
- `example/` — a standalone wgpu demo (macOS Metal)

## Build

```sh
zig build test          # host-target unit tests (WAV parser + module compile)
cd example && zig build  # the demo (macOS: links Metal/QuartzCore/Foundation)
```
