# 🔬 Oceanographic Data Research & Mathematical Calibration

This document outlines the background research, data sourcing parameters, and statistical validation frameworks driving the **Sagar-Drishti** ecosystem.

## 1. Data Ingestion Profile (INCOIS Ecosystem)
Our system is designed to interface with heterogeneous ocean telemetry metrics:
* **HYCOM Numerical Models:** Grid-based multi-variate continuous layers detailing global ocean state estimations.
* **In-Situ BUOY Feeds (Argo Floats / Gliders):** Irregularly distributed physical sensors logging true field parameters vertically through the water column.

## 2. The Vertical Alignment & Spline Interpolation Engine
When cross-referencing model forecasts with physical buoy readings, spatial-temporal gaps exist. Model metrics are locked to predefined depth tiers (e.g., Level 1 = 0m, Level 2 = 10m), whereas an Argo probe might log data at 4.7m.

### The Traceability Algorithm:
Instead of utilizing standard nearest-neighbor approximations which mask horizontal discrepancies, Sagar-Drishti implements **1D Cubic Spline Interpolation** directly over the localized vertical water column:

$$\Delta z = z_{buoy} - z_{model\_tier}$$

If $\Delta z \neq 0$, the platform computes an intermediate parameter matrix and explicitly tags the dashboard node with a **[TRACEABLE INTERPOLATION FLAG]**. This ensures researchers know exactly whether they are looking at raw extracted data or mathematically adjusted metrics.

## 3. Statistical Validation Metrics
To gauge model precision against real observations, the core computation module continuously solves for two primary error bounds:

### Root Mean Squared Error (RMSE):
$$RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(V_{model} - V_{observation})^2}$$

### Model Bias:
$$Bias = \frac{1}{n}\sum_{i=1}^{n}(V_{model} - V_{observation})$$

These metrics are dispatched as raw active arrays to the frontend to drive 5 dynamic validation charts via Chart.js.
