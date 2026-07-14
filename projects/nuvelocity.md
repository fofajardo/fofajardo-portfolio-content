---
tags: 
  - "personal"
  - "packages"
title: "NuVelocity"
subtitle: "Re-implementation of Reflexive Entertainment's Velocity Engine"
dateStart: "2023-07"
technologies: 
  - "cpp"
  - "sdl"
  - "csharp"
points: []
preview: "29"
links: 
  - type: "github"
    url: "https://github.com/NuVelocity/NuVelocity"
hasBody: true
---

NuVelocity (NV) is a C++ re-implementation of the Velocity Engine, the proprietary game engine developed by Reflexive Entertainment and used in games such as Ricochet Xtreme (2001). It was built on top of SDL3 and reconstructed through a combination of static and dynamic reverse engineering, including hex-editor analysis of the game's proprietary file formats and behavioral observation of the original executable. The engine reproduces the property management system, plugin architecture, rendering/layering, particle and physics subsystems, and power-up spawning logic of the original, and served as the foundation for a full re-implementation of Ricochet Xtreme itself.

NuVelocity's asset pipeline reverse engineers two proprietary image formats used by the Velocity Engine's cache: standalone "frame" files for static images, and "sequence" files for animated sprite sheets, texture atlases, and bitmap fonts. Both formats store pixel data using a planar (non-interleaved) RGBA layout with per-channel delta ('Sub' filter-style) encoding prior to DEFLATE compression, and support alternate JPEG-based sub-cases with a separately stored, DEFLATE-compressed alpha channel. It utilizes a [soft fork](https://github.com/NuVelocity/NuVelocity.physfs) of PhysFS to accommodate Reflexive Entertainment's modified ZIP archives, which replace the standard end-of-central-directory signature (`PK`) with `RE`. The project is designed for extensibility, performance, and strong type safety.

#### NuVelocitySharp

NuVelocitySharp was the prior attempt at re-implementing the engine in C#. The project has successfully decrypted and re-exported graphics assets from later Reflexive Entertainment games, such as [Ricochet Infinity](https://wiki.ricochetuniverse.com/wiki/Ricochet_Infinity) and [Ricochet HD](https://wiki.ricochetuniverse.com/wiki/Ricochet_HD). The aim is to revive these classic games for modern gamers while fostering a collaborative community of developers and enthusiasts.

The [NuVelocity Unpacker](https://github.com/frankwilco/NuVelocity.Unpacker/releases/latest), released in 2023, converts "frame" and "sequence" files back into TGA images and reconstructs their corresponding property files, and has been used to validate the recovered file format specification. It is already released to the public, along with a list of currently supported games.
