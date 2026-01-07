# GHZ200 Custom Stage Sandbox (Sonic Generations)

A custom stage replacement mod for **Sonic Generations (2011) PC** that replaces **Green Hill Zone – Act 2 (Modern)** (`ghz200`) with a free-roam sandbox stage.

This repo focuses on **project structure + documentation + reproducible pipeline**. Large binaries (exports, intermediate assets, base game files) should stay out of Git by default.

## What this mod replaces

- **Stage slot:** `ghz200` (Green Hill Zone Act 2 – Modern)

## Release folder structure (what players install)

Your published mod should look like:

```
GHZ200_CustomStage_Sandbox/
  mod.ini
  README.md
  CREDITS.md
  PERMISSIONS.md
  disk/
    bb/
      Packed/
        ghz200/
          ghz200.ar.00
          ghz200.arl
      #ghz200.ar.00
      #ghz200.arl
```

## Build / edit workflow

See: **PIPELINE.md**

## Third-party assets & permissions

This mod includes third-party assets that must be credited and/or used with permission.
See: **CREDITS.md** and **PERMISSIONS.md**.

## Disclaimer

Sonic Generations is © SEGA / Sonic Team.  
This is a fan-made mod, provided **non-commercially**, and is not affiliated with SEGA.

## Versioning

- Repo tags/releases should match the mod version in `mod.ini`.
- Keep a simple changelog in **CHANGELOG.md**.

---

If you're a player: download the **release .zip** from GameBanana (or GitHub Releases if you use them) and install via **HedgeModManager**.
