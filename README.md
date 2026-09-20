# CadRemesh

Feature-aware STEP-to-Blender quad retopology, packaged as a real Blender extension.

Every existing STEP import path for Blender works from an already-triangulated mesh — by the
time a typical retopology tool sees the geometry, the exact original CAD structure (fillets,
holes, flat faces) has already been thrown away by the tessellation step, and the tool has to
guess that structure back out of a triangle soup. CadRemesh reads the STEP file's real structure
directly and builds quad topology aligned to the actual feature boundaries, instead of
reverse-engineering it after the fact.

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

100% quad output, no triangles or n-gons, validated against a real 8-part mechanical assembly,
a medical-grade stent at 0.055mm feature scale, and everyday CAD parts (fans, power supplies,
linear guides).

## Availability

CadRemesh is a commercial Blender extension. Purchase and delivery details coming soon.

## License

GPL-2.0-or-later — required by Blender's own Python API licensing terms for any addon that
uses `bpy`. Full source is provided to purchasers along with their download.
