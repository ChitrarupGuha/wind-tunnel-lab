# Technical Limitations

**Project:** Wind Tunnel Lab  
**Version:** 1.0  
**Last updated:** 7 November 2026

## 1. Purpose of This Document

This document describes the known technical, numerical, and physical limitations of Wind Tunnel Lab.

Wind Tunnel Lab is an educational browser-based aerodynamic visualization project. Its current implementation uses a simplified two-dimensional incompressible stable-fluids solver alongside a separate vehicle-performance model.

The limitations documented here define the boundaries of the current implementation. They also identify areas requiring further investigation, testing, and development.

The purpose is to distinguish what the application currently demonstrates from what would require more rigorous numerical modelling or experimental validation.

## 2. Two-Dimensional Simulation

### Current limitation

The flow solver operates on a two-dimensional computational grid.

Real-world aerodynamic flows are three-dimensional. Fluid motion can vary across all three spatial dimensions, and important flow structures may extend beyond a two-dimensional plane.

### Consequences

- Three-dimensional flow structures are not represented.
- Spanwise flow and wingtip effects are absent.
- Three-dimensional separation and vortex structures cannot be accurately reproduced.
- The simulation cannot fully represent the aerodynamic behaviour of complex real-world objects.

### Future investigation

Explore whether a three-dimensional solver or a more advanced two-dimensional formulation is appropriate for the project's intended educational scope.

## 3. Simplified Incompressible Flow Model

### Current limitation

The solver uses a simplified incompressible stable-fluids approach.

This is useful for interactive visualization, but it does not represent every physical characteristic of real airflow.

The current implementation does not provide a complete, validated solution of the governing fluid-flow equations.

### Consequences

- Compressibility effects are not represented.
- Shock waves are not modelled.
- The solver does not provide a complete physical treatment of turbulent flow.
- Numerical diffusion can reduce the visibility and strength of flow structures.
- Results may differ significantly from real aerodynamic behaviour under conditions outside the model's assumptions.

### Future investigation

Document the governing assumptions more precisely and investigate more rigorous numerical methods for the intended operating conditions.

## 4. Numerical Diffusion and Effective Reynolds Number

### Current limitation

The semi-Lagrangian advection approach supports numerical stability, but it introduces numerical diffusion.

The implementation also includes vorticity confinement to help preserve rotational structures.

However, vorticity confinement is not a substitute for a physical turbulence model.

The effective Reynolds number of the numerical simulation is not independently controlled or demonstrated to match the Reynolds number calculated from the selected physical reference parameters.

### Consequences

- Small-scale flow structures may become smeared.
- Vortices may decay differently from their real-world counterparts.
- Flow separation and wake behaviour may not be physically accurate.
- Changing numerical settings may change the resulting flow patterns.

### Future investigation

- Study the effect of numerical diffusion.
- Examine sensitivity to solver parameters.
- Investigate numerical methods with more controlled physical viscosity.
- Compare simulated flow behaviour with suitable reference cases.

## 5. Pressure and Boundary-Condition Limitations

### Current limitation

The solver uses a custom pressure-correction procedure to reduce velocity divergence.

Its pressure-like field is not established as a calibrated dimensional pressure solution.

The current boundary handling is simplified and does not reproduce every physical inlet, outlet, wall, or obstacle condition.

### Consequences

- Pressure distributions may not correspond to real measured pressure.
- Boundary treatment may influence the flow field.
- Obstacle geometry and grid representation may affect local flow behaviour.
- Numerical errors may influence pressure-based force estimates.

### Future investigation

- Examine the pressure-correction procedure.
- Study divergence before and after pressure correction.
- Investigate boundary-condition sensitivity.
- Compare the numerical behaviour against established numerical test cases.

## 6. Grid Resolution and Numerical Sensitivity

### Current limitation

The current computational grid is fixed at 180 × 96 cells.

A grid-resolution experiment comparing 180 × 96 with 360 × 192 showed approximately 30% variation in the estimated drag coefficient.

This indicates that the current coefficient estimate is sensitive to numerical resolution.

### Consequences

- Estimated aerodynamic coefficients may change with grid resolution.
- Small geometric features may not be represented consistently.
- Obstacle boundaries are affected by rasterization.
- Numerical outputs cannot currently be considered grid-independent.

### Future investigation

Conduct systematic grid-resolution studies using multiple resolutions and identical simulation conditions.

A proper grid-convergence investigation should compare relevant quantities across progressively refined grids and document whether the results approach a stable value.

Until this is established, the displayed aerodynamic coefficients should be treated as approximate comparative indicators.

## 7. Aerodynamic Force Estimation

### Current limitation

The current implementation estimates aerodynamic force contributions using pressure-like values near obstacle-boundary cells.

The estimates are pressure-based and do not represent a complete integration of all aerodynamic stresses over a validated physical surface.

The force estimates are also two-dimensional and per-span in their intended interpretation.

### Consequences

- Viscous shear contributions are not fully represented.
- Force estimates depend on the pressure-like field and obstacle-boundary representation.
- Results may be sensitive to geometry rasterization and grid resolution.
- The estimates cannot be directly interpreted as validated full-scale vehicle or aircraft forces.

### Future investigation

- Investigate more complete surface-force integration.
- Separate pressure and viscous contributions.
- Define reference dimensions and areas consistently.
- Compare calculated forces with suitable analytical or experimental reference cases.

## 8. Physical Parameters and Reference Quantities

### Current limitation

The application calculates physical reference quantities such as air density, dynamic pressure, and Reynolds number using selected environmental and geometry parameters.

However, the solver's internal grid-space quantities are not fully calibrated against those physical reference quantities.

In particular, the current tunnel-speed control affects displayed physical calculations, while the solver uses a fixed reference inflow value (`Uc = 60`) in its grid-space simulation.

### Consequences

- The displayed physical airspeed is not directly coupled to the solver's actual inlet velocity.
- Calculated Reynolds number does not establish the effective Reynolds number of the numerical flow.
- Dynamic pressure calculations do not make the internal pressure-like field dimensionally validated.
- Physical interpretations of the visualized flow must remain limited.

### Future investigation

Establish a consistent relationship between physical units, grid spacing, time step, inlet velocity, viscosity, and derived aerodynamic quantities.

## 9. Geometry Representation

### Current limitation

Objects are represented through rasterized geometry masks on the computational grid.

The application supports predefined geometries, freehand drawing, scaling, and angle-of-attack adjustments.

However, rasterized boundaries do not provide the geometric precision of a high-quality computational mesh.

### Consequences

- Small features may disappear or become distorted.
- Curved surfaces are approximated by grid cells.
- Boundary representation changes with resolution.
- Geometry changes may influence numerical force estimates.

### Future investigation

Investigate improved boundary representations, sub-grid geometry handling, or mesh-based methods where appropriate.

## 10. Visualization Limitations

### Current limitation

The pressure and speed views use colour mapping to represent simulation fields. The streamline view uses particles that move through the sampled velocity field.

These are visualization techniques, not independent measurements of physical flow.

### Consequences

- Colour normalization may make different simulation states appear visually similar.
- Auto-scaling can make comparisons misleading without a shared scale.
- Particle trajectories depend on the underlying numerical velocity field.
- Visual similarity to experimental flow patterns does not establish numerical accuracy.

### Future investigation

- Provide clearer scale information.
- Support consistent colour ranges for comparisons.
- Improve visualization of numerical uncertainty.
- Distinguish normalized visualization values from dimensional physical quantities.

## 11. Vehicle Performance Model

### Current limitation

The vehicle-performance subsystem is a simplified mathematical model.

It includes throttle, RPM, gear shifting, turbo boost, NOS activation, engine stress, and estimated vehicle motion.

It is separate from the core flow solver rather than being a fully coupled vehicle-aerodynamics simulation.

### Consequences

- Engine behaviour is not based on a complete thermodynamic model.
- Turbocharger behaviour is simplified.
- NOS power delivery and engine stress are approximations.
- Vehicle parameters are configured model values, not verified manufacturer specifications.
- Vehicle motion estimates should not be interpreted as measured or validated performance.
- Aerodynamic and powertrain calculations do not constitute a complete physical vehicle model.

### Future investigation

Improve the separation of powertrain and aerodynamic calculations, document the assumptions of each subsystem, and investigate more realistic vehicle-dynamics models.

## 12. Performance and Computational Constraints

### Current limitation

The application runs its simulation and rendering workloads in the browser.

Performance depends on the user's hardware, browser, display resolution, and other active processes.

The adaptive quality system adjusts particle count and solver iterations to manage computational workload.

However, adaptive rendering quality does not increase the underlying grid resolution or guarantee numerical accuracy.

### Consequences

- Performance varies across devices.
- Lower quality settings may reduce visualization detail.
- High simulation workloads may affect responsiveness.
- Browser limitations can constrain the complexity of future numerical models.

### Future investigation

Explore optimized numerical operations, more efficient memory handling, and optional worker-based computation where appropriate.

## 13. Validation Status

### Current status

Wind Tunnel Lab has not been established as an experimentally validated CFD application.

The current implementation does not have documented validation against physical wind-tunnel measurements or a completed comparison against accepted CFD benchmark cases.

The observed grid-resolution sensitivity further indicates that numerical verification remains necessary.

### Future validation strategy

A systematic evaluation should include:

1. **Numerical verification:** Examine whether the implementation behaves consistently with its intended mathematical formulation.
2. **Grid sensitivity:** Compare results across multiple grid resolutions.
3. **Benchmark comparison:** Evaluate appropriate simplified geometries against publicly available reference cases.
4. **Physical comparison:** Where suitable data is available, compare numerical results with experimental measurements.
5. **Reproducibility:** Document geometry, boundary conditions, solver settings, and calculation methods for every comparison.

Verification and validation are different activities. A solver may correctly implement its intended numerical method without accurately representing real-world experimental behaviour.

## 14. Interpretation Guidelines

Until the limitations above are addressed, users should interpret Wind Tunnel Lab outputs as follows:

| Output | Recommended interpretation |
|---|---|
| Pressure view | Relative visualization of a pressure-like field |
| Speed view | Relative visualization of simulated velocity magnitude |
| Streamline view | Visual representation of sampled velocity trajectories |
| Drag coefficient | Approximate, resolution-sensitive estimate |
| Lift coefficient | Approximate, resolution-sensitive estimate |
| Drag and lift forces | Simplified pressure-based estimates |
| Reynolds number | Calculated physical reference quantity, not proof of numerical flow equivalence |
| Vehicle performance | Simplified interactive model output |

These outputs are suitable for educational exploration, but not as standalone evidence for real-world engineering decisions.

For the complete intended-use and safety boundaries, refer to the project's `DISCLAIMER.md`.

## 15. Development Priorities

The following areas are identified for future technical investigation.

| Priority | Area | Objective |
|---|---|---|
| High | Physical scaling | Establish consistent physical and numerical reference quantities |
| High | Grid sensitivity | Investigate resolution dependence and convergence |
| High | Pressure correction | Examine numerical behaviour and divergence reduction |
| High | Force estimation | Improve the calculation and interpretation of aerodynamic forces |
| Medium | Boundary conditions | Investigate more appropriate inlet, outlet, and wall treatments |
| Medium | Geometry representation | Improve obstacle-boundary accuracy |
| Medium | Benchmark testing | Compare against suitable reference cases |
| Medium | Visualization | Improve scales and comparison consistency |
| Low | Browser optimization | Improve performance and computational efficiency |

These priorities describe possible development work, not completed features or guaranteed outcomes.

---

**Wind Tunnel Lab**  
An independent educational aerodynamics simulation project.

**Author:** Chitrarup Guha  
**Repository:** https://github.com/ChitrarupGuha/wind-tunnel-lab
