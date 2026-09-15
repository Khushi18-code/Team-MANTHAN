# 🎨 Sagar-Drishti Frontend Graphics & Rendering Engine
> **A Deep Dive into WebGL, Custom GPU Shaders, Raycasting Interactivity, and Dynamic Charting**

This document details the low-level graphics pipeline, rendering strategies, and engineering choices that allow **Sagar-Drishti** to deliver immersive, 60 FPS ocean datasets directly in the client browser with zero installation overhead.

---

## 🗺️ Browser Rendering Pipeline

```mermaid
graph TD
    %% Ingestion
    subgraph IN["Data Ingestion"]
        A[JSON Multi-Matrix Payload] -->|Asynchronous Fetch| B[App State Controller]
    end

    %% GPU Pipeline
    subgraph GPU["GPU Graphics Pipeline (WebGL2 / Three.js)"]
        B -->|Volumetric Matrix Buffers| C[Three.js Scene Setup]
        C -->|Inject Static Coordinates| D[Custom Vertex Shaders]
        C -->|Inject Real-time Value Arrays| E[Custom Fragment Shaders]
        D -->|Hardware Level Matrix Transforms| F[GPU Graphics Memory]
        E -->|60 FPS Continuous Gradient Painting| F
        F --> G[(True 3D Ocean Water Column Canvas)]
    end

    %% Interaction Loop
    subgraph INT["Real-Time Interaction Loop"]
        H[User Viewport Click] -->|Screen Coordinates| I[GPU Raycasting Engine]
        I -->|Project Vector Intersection| J{Mesh Target Intersected?}
        J -->|Argo Node Detected| K[Extract Float Metadata]
        K -->|Trigger Dynamic Target Re-route| L[5 Live Comparative Analytics Charts]
    end

    %% Chart Pipeline
    subgraph CRT["Statistical UI Layer"]
        L --> M[Chart.js Pipeline Engine]
        B -->|Raw Metrics Stream| M
        M -->|Plot RMSE, Bias, and Deltas| N[Interactive Dashboards]
    end

    style IN fill:#009688,stroke:#fff,stroke-width:2px,color:#fff
    style GPU fill:#1a73e8,stroke:#fff,stroke-width:2px,color:#fff
    style INT fill:#ea4335,stroke:#fff,stroke-width:2px,color:#fff
    style CRT fill:#34a853,stroke:#fff,stroke-width:2px,color:#fff
```

---

## ⚙️ Low-Level Technical Mechanics & Justifications

### 📍 1. True 3D Volumetric Rendering (WebGL & Three.js)
* **The Core Mechanic:** Instead of rendering flat 2D maps or standard charts, the frontend utilizes **WebGL** via **Three.js** to build an interactive, volumetric representation of the ocean water column (similar to the technology stack driving Google Earth).
* **Reasoning:** Oceanography parameters dynamically morph based on depth variations. A true 3D spatial space allows researchers to manually twist, turn, zoom, and inspect deep ocean variables alongside the physical trajectories of Argo floats simultaneously in one workspace.

### 📍 2. Real-Time Hardware Gradients (Custom GLSL Shaders)
* **The Core Mechanic:** We bypassed standard CPU plotting loops and wrote custom **GLSL (OpenGL Shading Language)** Vertex and Fragment shaders that compile and execute directly on the user's GPU graphics processing units.
* **Reasoning:** Standard CPU rendering chokes and lags when plotting thousands of multi-dimensional matrix points. By uploading raw temperature and salinity arrays straight to the GPU, our fragment shader automatically paints smooth, continuous color vector fields at a locked **60 Frames Per Second (FPS)** refresh rate, even on standard consumer laptops or mobile screens.

### 📍 3. Low-Latency Interactivity (GPU Raycasting)
* **The Core Mechanic:** When a user clicks anywhere on the 3D scene canvas to inspect a floating target node, the engine utilizes a **Raycaster matrix transform**. It projects an imaginary 3D geometric ray vector from the exact 2D camera viewport click point into the active 3D world scene grid.
* **Reasoning:** Bypassing traditional flat search loops across large arrays, raycasting identifies instantly which specific **Argo Float asset vector mesh** was intersected by the pointer, pulling up its local profile, historical tracking trajectory, and provenance parameters on the fly.

### 📍 4. Multi-Variant Statistical Displays (Chart.js Engine)
* **The Core Mechanic:** Upon selecting an active float node, the user enters the model-versus-observation workspace. The system loads data metrics asynchronously into **Chart.js** pipelines to plot **5 live comparative analytics charts**.
* **Reasoning:** These dashboards graphically display model outputs against true physical buoy readings, showcasing raw deviations, delta changes, and calculated verification thresholds (RMSE and Bias) in a clean, interactive canvas layout.
