# CadRemesh

Feature-aware STEP-to-Blender quad retopology, packaged as a real Blender extension.

Every existing STEP import path for Blender works from an already-triangulated mesh — by the
time a typical retopology tool sees the geometry, the exact original CAD structure (fillets,
holes, flat faces) has already been thrown away by the tessellation step, and the tool has to
guess that structure back out of a triangle soup. CadRemesh reads the STEP file's real structure
directly and builds quad topology aligned to the actual feature boundaries, instead of
reverse-engineering it after the fact — the first packaged, one-click Blender addon built this
way. Every other Blender-side tool (Quad Remesher, Quadify, Smart Remesh) works from the
tessellated mesh, same as everything else.

## Before / after

Same real part, same view. A typical triangulated import versus CadRemesh's output:

| Generic triangulated import | CadRemesh output |
|---|---|
| ![Triangulated](images/triangulated-generic.png) | ![Quad topology](images/quad-topology.png) |

Same comparison on a real 8-part mechanical assembly — more surface complexity, still clean quads:

| Generic triangulated import | CadRemesh output |
|---|---|
| ![Triangulated assembly](images/triangulated-generic-assembly.png) | ![Quad topology assembly](images/quad-topology-assembly.png) |

## Why it matters

Built for rendering and product animation, not game-asset poly budgets — no aggressive stripping
needed. Full density straight off Import is genuinely usable for this work, not something you
have to fight down to a workable size first.

- **Shades correctly** — quad topology reads clean under Shade Smooth, no faceting or pinched
  shading from irregular triangulation.
- **Subdivision-ready** — Catmull-Clark subdivision behaves the way it's supposed to on quads;
  triangles don't subdivide predictably.
- **Deforms better** — quad topology holds its shape more predictably under bending and
  animation than a triangulated mesh.
- **Skips the retopology tax** — most STEP imports need a manual cleanup pass before they're
  usable for a render. This one doesn't.

## What it does

- **Import STEP** — one Blender object per real solid body in the file, correctly named from
  the STEP label where available. Multi-part assemblies are split and named automatically.
- **Adjust Density** — retarget the quad count up or down at any time, always working from a
  never-touched backup of the original full-fidelity import so repeated adjustments never
  compound quality loss.
- **Real-world scale** — imports land at correct real-world Blender units automatically,
  regardless of the source file's own unit convention.
- **Clean Up Topology** — an optional pass that improves problem areas of the mesh, only
  keeping a change when it measurably helps — otherwise it's left alone.
- **Smooth Size Transition** — an opt-in option for a more gradual, less "algorithmic-looking"
  density falloff between fine and coarse areas of the mesh.

Import and Adjust Density produce 100% quad output — no triangles or n-gons — validated against
a real 8-part mechanical assembly, a medical-grade stent at 0.055mm feature scale, and everyday
CAD parts (fans, power supplies, linear guides). Clean Up Topology is the one exception: it can
turn a small number of neighboring quads into triangles or n-gons as a side effect of removing
genuinely degenerate faces — an explicit, disclosed tradeoff of that optional step, not the
normal result.

## Availability

CadRemesh is a commercial Blender extension. Purchase and delivery details coming soon.

## License

GPL-2.0-or-later — required by Blender's own Python API licensing terms for any addon that
uses `bpy`. Full source is provided to purchasers along with their download.
