# Technical Overview

**Project:** Wind Tunnel Lab  
**Version:** 1.0  
**Author:** Chitrarup Guha  
**Repository:** https://github.com/ChitrarupGuha/wind-tunnel-lab

## 1. Project Overview

Wind Tunnel Lab is a browser-based, interactive educational environment for exploring simplified aerodynamic behaviour and vehicle performance.

The application combines a custom two-dimensional incompressible stable-fluids solver with a separate vehicle powertrain model. Users can select predefined geometries, draw custom shapes, adjust simulation parameters, and observe changes in airflow visualizations and estimated aerodynamic quantities.

The project is designed to make aerodynamic concepts interactive and accessible without requiring specialized desktop simulation software.

### Primary Objectives

- Visualize simplified two-dimensional airflow around objects.
- Explore pressure and velocity-field representations.
- Experiment with object geometry and angle of attack.
- Observe approximate drag and lift behaviour.
- Explore Reynolds number and dynamic pressure calculations.
- Demonstrate a simplified vehicle powertrain with turbo boost and nitrous oxide (NOS) controls.
- Provide an interactive environment for experimentation and learning.

## 2. System Architecture

The application currently runs entirely in the browser using HTML, CSS, and JavaScript.

There is no separate application server or backend required for the current implementation.

### Main Components

```text
Wind Tunnel Lab
│
├── User Interface
│   ├── Vehicle and geometry presets
│   ├── Design and drawing tools
│   ├── Wind and environmental controls
│   ├── Simulation quality controls
│   └── Vehicle performance controls
│
├── Geometry System
│   ├── Preset geometry generation
│   ├── Custom drawing and erasing
│   ├── Angle of attack transformation
│   ├── Model scaling
│   └── Solid-boundary mask generation
│
├── Flow Simulation
│   ├── Velocity fields (u, v)
│   ├── Pressure-like field
│   ├── Boundary and obstacle masks
│   ├── Pressure correction
│   ├── Semi-Lagrangian advection
│   └── Vorticity confinement
│
├── Visualization
│   ├── Pressure-field rendering
│   ├── Speed-field rendering
│   ├── Flow-particle trajectories
│   └── Geometry and ground-plane rendering
│
├── Aerodynamic Calculations
│   ├── Pressure-based force estimates
│   ├── Drag coefficient (Cd)
│   ├── Lift coefficient (Cl)
│   ├── Dynamic pressure
│   └── Reynolds number
│
└── Vehicle Performance Model
    ├── Throttle and RPM
    ├── Gear shifting
    ├── Turbo boost
    ├── NOS activation logic
    ├── Engine stress
    └── Estimated vehicle motion
```

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| HTML5 | Application structure |
| CSS3 | Interface styling and responsive layout |
| JavaScript | Simulation logic and application behaviour |
| HTML Canvas 2D | Geometry, fields, particles, and visual rendering |
| Typed Arrays | Numerical field storage |
| Path2D | Efficient flow-trail rendering |
| RequestAnimationFrame | Browser animation and simulation loop |

The numerical arrays primarily use `Float32Array` for continuous simulation fields and `Uint8Array` for boundary classification.

The application uses multiple off-screen canvases to prepare geometry masks, rendered fields, and visual overlays before displaying them on the main canvas.

## 4. Computational Domain and Grid

The current simulation canvas uses the following internal dimensions:

| Parameter | Value |
|---|---:|
| Canvas width | 900 pixels |
| Canvas height | 480 pixels |
| Grid cell size | 5 pixels |
| Grid width | 180 cells |
| Grid height | 96 cells |
| Total grid cells | 17,280 |

The computational domain is represented by a two-dimensional rectangular grid.

Each cell stores information used by the simulation, including velocity components, pressure-like values, and solid-boundary information.

### Main Simulation Fields

| Field | Representation | Purpose |
|---|---|---|
| `u` | Float32Array | Horizontal velocity component |
| `v` | Float32Array | Vertical velocity component |
| `p` | Float32Array | Pressure-like field |
| `s` | Float32Array | Fluid and solid-cell mask |
| `bd` | Uint8Array | Obstacle-boundary marker |
| `om` | Float32Array | Vorticity-related field |

The solver uses a staggered arrangement for velocity sampling, with horizontal and vertical components sampled at different positions relative to grid cells.

The geometry mask determines which regions are treated as solid obstacles and which remain available for fluid calculations.

## 5. Flow Simulation Method

The flow simulation is implemented through a custom simplified incompressible stable-fluids approach.

The solver maintains horizontal and vertical velocity fields and updates them over discrete time steps.

Its current implementation includes the following operations:

### 5.1 Inflow and Boundary Handling

The simulation introduces horizontal inflow at the upstream boundary.

Velocity values are assigned at the inlet, while downstream and domain-edge values are handled using simplified boundary updates.

The geometry mask prevents ordinary fluid updates from being applied inside solid obstacle cells.

A ground-plane option can also restrict the lower portion of the computational domain.

### 5.2 Pressure Correction

The solver calculates a divergence-related correction from neighbouring velocity values.

An iterative correction procedure updates the pressure-like field and adjusts neighbouring velocity components.

This is intended to reduce local velocity divergence and produce a more stable flow field.

The implementation is a custom approximation. It should not be interpreted as a fully validated pressure-Poisson CFD solver.

### 5.3 Semi-Lagrangian Advection

The solver transports velocity information through the grid using a semi-Lagrangian sampling approach.

Instead of directly moving grid cells, it traces backward through the velocity field to estimate where information originated.

Bilinear interpolation is used to sample values at non-integer grid positions.

This approach helps maintain numerical stability during interactive simulation, although numerical diffusion remains a limitation.

### 5.4 Vorticity Confinement

The solver includes an optional vorticity-confinement operation.

It estimates local rotational behaviour and applies a correction intended to preserve or enhance vortical structures that may otherwise become numerically diffused.

The strength of this operation can be adjusted through the user interface.

It is a visual and numerical enhancement, not a complete physical turbulence model.

### 5.5 Simulation Time Stepping

The simulation advances using discrete time steps.

The main animation loop uses a nominal simulation step of approximately 1/60 second and limits the number of accumulated simulation steps processed in one browser frame.

This helps prevent large simulation backlogs when rendering performance drops.

## 6. Geometry and Obstacle System

The geometry system allows users to experiment with predefined and custom objects.

### Available Presets

| Preset | Description |
|---|---|
| Car | Simplified car-like geometry |
| Bike | Simplified motorcycle geometry |
| Plane | Aircraft-like geometry |
| Wing | Airfoil-like geometry |
| Laval nozzle | Converging-diverging passage |
| Blank | Empty geometry for custom designs |

Preset geometries are drawn onto an off-screen canvas.

The geometry can be transformed through:

- Angle of attack adjustment.
- Model scaling.
- Ground-plane selection.
- Freehand drawing.
- Erasing.
- Clearing the current geometry.

After a geometry change, the application rebuilds its obstacle mask.

The mask is converted into a grid representation, allowing the solver to distinguish between fluid cells and solid regions.

Custom geometry is therefore represented through a rasterized grid mask rather than a detailed three-dimensional surface mesh.

## 7. Visualization System

The application provides three primary visualization modes.

### 7.1 Pressure View

Displays a colour-mapped representation of the pressure-like field.

The visualization uses a blue-to-cyan-to-green-to-yellow-to-red colour lookup table.

Pressure values are auto-scaled relative to the simulation state. The displayed colours should not be interpreted as calibrated pressure measurements in Pascals.

### 7.2 Speed View

Displays a colour-mapped representation of local velocity magnitude.

The velocity magnitude is estimated from the horizontal and vertical velocity components.

The displayed field is normalized relative to the simulation's reference inflow scale.

### 7.3 Streamline View

Displays particle trajectories through the simulated velocity field.

Particles are advanced using sampled velocity values and maintain short trajectory histories for rendering.

The particles are visual tracers. They are not independent physical particles, and their number does not represent the actual number of fluid particles in the domain.

### Rendering Pipeline

```text
Simulation Fields
       │
       ▼
Field Sampling
       │
       ▼
Colour Mapping
       │
       ▼
Off-screen Canvas
       │
       ▼
Particle Trajectories
       │
       ▼
Geometry and Ground Plane
       │
       ▼
Main Canvas Rendering
```

## 8. Aerodynamic Calculations

The application calculates or displays several aerodynamic quantities using simplified relationships.

### 8.1 Air Density

Air density is estimated using the ideal-gas relationship:

\[
\rho = \frac{p}{R T}
\]

Where:

- \(\rho\) = air density
- \(p\) = assumed atmospheric pressure
- \(R\) = specific gas constant for dry air
- \(T\) = absolute temperature in Kelvin

The current implementation assumes atmospheric pressure of 101325 Pa.

### 8.2 Dynamic Pressure

\[
q = \frac{1}{2}\rho V^2
\]

Where:

- \(q\) = dynamic pressure
- \(\rho\) = estimated air density
- \(V\) = selected reference airspeed

### 8.3 Reynolds Number

\[
Re = \frac{\rho V L}{\mu}
\]

Where:

- \(Re\) = Reynolds number
- \(\rho\) = estimated air density
- \(V\) = reference airspeed
- \(L\) = reference geometry length
- \(\mu\) = dynamic viscosity

Dynamic viscosity is estimated using Sutherland's formula.

### 8.4 Drag and Lift Relationships

The application uses the conventional aerodynamic relationships as a reference:

\[
F = q C A_{\mathrm{ref}}
\]

Where:

- \(F\) = estimated aerodynamic force
- \(q\) = dynamic pressure
- \(C\) = drag or lift coefficient
- \(A_{\mathrm{ref}}\) = reference area

However, the coefficients generated by the current solver are approximate, pressure-based, and two-dimensional.

They are not equivalent to experimentally established three-dimensional aerodynamic coefficients.

### 8.5 Pressure-Based Coefficient Estimates

The solver estimates force contributions by examining pressure-like values adjacent to obstacle-boundary cells.

The resulting horizontal and vertical force estimates are normalized using a reference quantity to obtain approximate Cd and Cl values.

The implementation also maintains a rolling history of coefficient estimates over the last 240 simulation steps and displays their mean and standard deviation.

**Important:** The solver's internal pressure-like field and force normalization are not a calibrated dimensional pressure-and-force solution. The separately calculated dynamic pressure displayed in Pascals does not make the internal pressure field dimensionally validated.

## 9. Vehicle Performance Model

Wind Tunnel Lab also contains an experimental vehicle-performance subsystem.

This subsystem is separate from the core flow solver. It models simplified vehicle motion and engine behaviour using preset vehicle parameters and estimated aerodynamic quantities.

### 9.1 Vehicle Parameters

Each preset has its own configured values, including:

- Vehicle mass.
- Base engine horsepower.
- Approximate maximum speed.
- Rolling-resistance coefficient.
- Reference geometry depth.
- Reference length scale.

These are simplified model parameters, not manufacturer-verified specifications.

### 9.2 Throttle and Engine RPM

Throttle input can be controlled using on-screen buttons or keyboard controls.

The model estimates engine RPM from vehicle velocity and the selected gear ratio.

It also includes automatic gear-up and gear-down conditions based on RPM thresholds.

### 9.3 Turbo Boost

The turbo subsystem calculates a simplified boost response based on throttle input, engine RPM, and the selected maximum boost setting.

Boost influences the estimated engine power output.

This is an interactive performance model, not a detailed thermodynamic turbocharger simulation.

### 9.4 Nitrous Oxide (NOS)

The NOS subsystem uses a set of activation conditions.

The solenoid activates only when all configured conditions are satisfied:

1. ARM switch enabled.
2. Throttle above 80%.
3. Engine RPM above 3500.
4. Boost reaches the configured staging threshold.
5. NOS bottle has remaining capacity.
6. NOS activation button is held.

Available shot settings are 50, 100, 150, and 200 horsepower.

The subsystem also estimates engine stress and applies simplified power reduction and knock behaviour when stress reaches its threshold.

### 9.5 Vehicle Motion

The vehicle model estimates acceleration using a simplified force balance involving:

- Estimated engine driving force.
- Estimated aerodynamic drag.
- Rolling resistance.
- Vehicle mass.

The resulting velocity is updated over time.

The powertrain and vehicle model are intended for interactive experimentation, not real-world vehicle performance prediction.

## 10. Performance and Adaptive Quality

The application uses browser animation timing and adaptive rendering quality to balance visual performance with computational workload.

### Quality Settings

| Setting | Particle Count | Solver Iterations |
|---|---:|---:|
| Low | 1,200 | 12 |
| Medium | 3,200 | 20 |
| High | 7,000 | 32 |
| Auto | Dynamically adjusted | Dynamically adjusted |

In Auto mode, the application monitors recent processing time and frame rate.

It adjusts particle count and solver iterations within configured limits to reduce workload when performance becomes constrained.

Particles are primarily a visualization workload. Increasing their count does not increase the numerical resolution of the flow grid.

The grid resolution remains fixed at 180 × 96 in the current implementation.

## 11. Current Technical Boundaries

The current implementation has several known limitations:

- Two-dimensional simulation only.
- Simplified incompressible flow representation.
- Numerical viscosity is present, and effective Reynolds number is not controlled.
- No fully validated pressure-Poisson CFD implementation.
- No physical turbulence model.
- No established experimental wind-tunnel validation.
- Pressure-based force estimates only.
- No demonstrated grid convergence.
- Numerical outputs depend on simulation settings and grid resolution.
- The vehicle powertrain uses simplified assumptions.
- Flow visualization and vehicle-performance calculations are not a fully coupled physical model.

A documented grid-resolution test showed approximately 30% variation in estimated Cd when changing the grid from 180 × 96 to 360 × 192.

This sensitivity is an important reason to treat the current aerodynamic coefficients as relative educational estimates rather than reliable engineering measurements.

Further details are maintained in `docs/limitations.md`.

## 12. Development Direction

Future development may investigate:

- Improved numerical stability and boundary handling.
- More systematic solver verification.
- Grid-resolution sensitivity studies.
- Comparison against publicly available benchmark cases.
- Improved aerodynamic force estimation.
- Better separation of visualization parameters and physical reference quantities.
- More transparent reporting of simulation assumptions.
- Additional educational geometries and visualization tools.

Any future claim of improved physical accuracy or validation should be supported by documented testing and reproducible results.

## 13. Technical References and Further Reading

The following resources provide useful foundations for understanding the numerical and physical concepts relevant to this project:

1. Jos Stam, *Stable Fluids*, Proceedings of SIGGRAPH 1999.  
   https://doi.org/10.1145/311535.311548

2. NASA Glenn Research Center, *Beginner's Guide to Aeronautics*.  
   https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/

3. NASA Glenn Research Center, *Reynolds Number*.  
   https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/reynolds-number/

4. NASA Glenn Research Center, *Drag Equation*.  
   https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/drag-equation/

These references provide background knowledge and do not constitute validation or endorsement of Wind Tunnel Lab.

---

**Wind Tunnel Lab**  
An independent educational aerodynamics simulation project.

**Author:** Chitrarup Guha  
**Repository:** https://github.com/ChitrarupGuha/wind-tunnel-lab
