# ⚙️ Sagar-Drishti System Architecture Blueprint

This blueprint describes the zero-build, low-latency execution pipeline engineered to render high-capacity multi-dimensional grids smoothly in standard portable browsers.

## 1. Zero-Build Frontend Strategy
* **Core Principle:** Vanilla WebGL wrapped via Three.js layer setups. No compilation pipelines, no React build steps, no bundle minification overheads.
* **Why?** Guarantees zero installation barrier, lightning-fast first contentful paint (FCP), and native reviewability during high-pressure evaluation windows.

## 2. GPU-Accelerated Graphic Shaders
To maintain a continuous **60 Frames Per Second (FPS)** rate while parsing dense volumetric coordinate matrices, visual property processing is offloaded from the CPU directly into the graphics hardware.
* **Vertex Shaders:** Map dynamic spatial grid coordinates based on targeted region and depth selections.
* **Fragment Shaders:** Handle real-time color vector interpolation (GLSL) to smoothly paint Temperature fields, Salinity vectors, and Chlorophyll densities into a gradient mesh.

## 3. Interaction Loops via GPU Raycasting
Mapping a user's 2D pointer coordinates on a display to an exact 3D floating point target (like an active Argo float marker) bypasses traditional flat searching arrays. The system utilizes low-latency ray selection vectors projecting intersections through active 3D node meshes instantly.
