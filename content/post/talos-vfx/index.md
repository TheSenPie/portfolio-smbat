+++
author = "Smbat Voskanyan"
title = "Talos VFX"
date = "2023-07-23"
description = "Enhancing Talos VFX: My Open-Source Contributions."
categories = [
    "Game Engine Dev"
]
tags = [
    "Java",
    "LibGDX",
]
image = "talos.png"
+++

# Introduction
Talos VFX is a powerful open-source visual effects editor designed for Java and LibGDX projects. Create stunning particles, shaders, and custom scripts, while seamlessly managing game assets – all from a single workspace. Its intuitive, node-based VFX editor and support for visual programming routines (similar to Unreal Engine's blueprints) empower you to craft dynamic effects. Build 2D levels and scenes with brushes, and bring your creations to life with Spine2d skeletal animations, easily attaching VFX directly to animation bones. While primarily focused on 2D, Talos VFX also offers limited 3D support.

As a major contributor to Talos VFX, I've played a role in squashing critical bugs, implementing user-requested features, and refining the overall user experience. As of writing this post I authored around ~50% of Pull Requests on the project. Here's the [link to project](https://github.com/rockbite/talos/tree/talos-3d). Note, that active development is carried on  `talos-3d` branch and `master` branch is greatly behind.

# Feature Development
Since a lot of features where missing initally and we needed many tools for our prototypes, I had a chance to contribute a lot in this area.

## Fake BVB" (Bone Attachment Support)
Problem: Users were limited in how they could interact with skeletal animations, hindering dynamic effects and customization.
Your Solution: Implemented "Fake BVB" functionality, exposing animation bones as restricted game objects within Talos, enabling the attachment of other objects.
Result: Users can now create more complex and visually engaging effects by directly linking particles, objects, and more to 
skeletal animations. Examples include attaching characters to moving vehicles or syncing particle effects to bone movements.

## NineSlices Support and Sprite Editor
Problem: Users lacked advanced scaling options for UI and graphic elements, limiting design flexibility. Limited or inefficient tools for sprite editing and managing NineSlice metadata within Talos VFX.
Your Solution: Implemented NineSlice rendering functionality, providing a system similar to Unity's NineSlices. This allows specific sections of images to be repeated horizontally, vertically, or in both directions.
Result: Improved control over how UI elements and graphics scale, enhancing the ability to create visually polished and responsive interfaces within Talos VFX.

# Bug Fixes and Refinements
I have fixed more bugs I could remember, however to recall some off top of my head, then these would be the ones.

## Project Explorer Stability and User Experience
Problem: File management was unreliable, with crashes and unexpected behaviors. Crashes when moving or renaming files. Bad user experience. Poor file search performance. 
Your Solution: Revamped project explorer logic, preventing errors and ensuring a smoother file management experience. Refreshed the UI for more costumization and assetes previews. Fast asset lookup.
Result: Increased stability and reliability within Talos VFX, protecting user work. Happy users.

## Routine Workflow
Problem: Editing curves within the Routine App was buggy, hindering intuitive workflow.
Your Solution: Fixed curve gizmo display and interaction points, including inserting new points and using the ESC key.
Result: Restored smooth and predictable curve editing, streamlining the creation of dynamic effects within routines.

# Concusion
Through this project, I've learned many new topics and significantly improved my knowledge in Java, libGDX, and 2D engine development tools. It was both challenging and rewarding to work with a community of people directly affected by my contributions. Seeing others use Talos VFX to create amazing games is a deeply satisfying experience.

{{< css.inline >}}
<style>
.canon { background: white; width: 100%; height: auto; }
</style>
{{< /css.inline >}}
