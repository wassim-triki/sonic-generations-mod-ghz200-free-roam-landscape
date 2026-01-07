# PIPELINE (ghz200 custom stage)

This is the repeatable pipeline we follow to go from Blender → in-game stage.

## Naming conventions

- Stage ID: `ghz200`
- Working folder (local only): `_WORKSPACE/`
- Release folder: `_RELEASE/` (the folder you zip for players)

## Required stage files (Generations)

For a custom stage replacement to load correctly, you typically ship:

- `disk/bb/Packed/ghz200/ghz200.ar.00`
- `disk/bb/Packed/ghz200/ghz200.arl`
- `disk/bb/#ghz200.ar.00`
- `disk/bb/#ghz200.arl`

The `Packed/ghz200` archive contains terrain/models/materials and stage data.
The `#ghz200` archive contains stage “support” data that the game expects to exist next to Packed.

## 0) One-time: project skeleton

- Make sure your mod has `mod.ini` and a `disk/bb/` folder.
- Keep big source assets outside Git, or under Git LFS if you really want them versioned.

## 1) Blender → FBX export

In Blender:
- Apply transforms (Ctrl+A → **Rotation & Scale**) on export collections/objects.
- Keep origin sensible (world origin is fine).
- Export FBX (selected objects is fine; no need to export lights/cameras).

Texture approach that behaves well with Hedgehog Converter:
- Put textures in a folder named `<fbx_name>_tex/` next to the FBX, e.g.
  - `my_map.fbx`
  - `my_map_tex/terrain_albedo.png`, `terrain_normal.png`, `terrain_roughness.png`, ...

Keep material graphs simple:
- One Principled BSDF
- Image textures plugged into Base Color / Normal (via Normal Map node) / Roughness.

## 2) Collision generation

Export collision mesh as FBX (often a simplified version).
Generate:
- `collision.phy.hkx` (plus any helper collision exports your tools produce)

## 3) Hedgehog Converter (FBX → terrain + archives)

In Hedgehog Converter:
- Game Engine: **Generations**
- Source model: your `<map>.fbx`
- Source textures directory: folder that contains your `<map>_tex/` and/or texture files
- Output: `_RELEASE/disk/bb/Packed/ghz200/`

Run Convert.

Verify the log detects your diffuse/albedo texture and writes a `.material` + `.dds` outputs.

## 4) SonicGLvl stage data (spawn, skybox, etc.)

Open stage in SonicGLvl:
- Ensure `SonicSpawn` exists and position is correct
- Save stage data (writes Stage files)

If you want GHZ sky:
- Copy the skybox model(s) + materials + textures that the stage references
- Repack after edits

## 5) Pack + test

- Ensure `_RELEASE` contains:
  - `disk/bb/Packed/ghz200/*`
  - `disk/bb/#ghz200.*`
  - `mod.ini`, README, CREDITS, PERMISSIONS

Test via HedgeModManager:
- Drag the mod folder or zip into HMM
- Enable, Save and Play
- Load GHZ Act 2 Modern

## Troubleshooting quick hits

- “Textures don’t show”:
  - Simplify material graph
  - Ensure texture folder is `<fbx_name>_tex/` next to FBX
  - Confirm converter log lists your diffuse texture (Assimp Type: 1)

- “Crashes on load after adding files”:
  - You likely shipped incomplete/mismatched materials/models referenced by Stage data.
  - Add assets through SonicGLvl (Material Editor) whenever possible.
