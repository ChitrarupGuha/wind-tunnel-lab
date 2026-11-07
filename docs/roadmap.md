# Development Roadmap

**Project:** Wind Tunnel Lab  
**Current Version:** 1.0  
**Author:** Chitrarup Guha  
**Repository:** https://github.com/ChitrarupGuha/wind-tunnel-lab

## 1. Vision

Wind Tunnel Lab aims to evolve from an interactive educational aerodynamics visualization into a more technically rigorous environment for exploring fundamental fluid-flow and aerodynamic concepts.

The development philosophy is to prioritize engineering correctness, reproducibility, and transparent numerical behaviour over visual complexity alone.

Future improvements will focus on understanding the limitations of the current implementation, improving its numerical foundations, and evaluating its behaviour against appropriate reference cases.

This roadmap represents development intentions, not guaranteed features or delivery dates.

## 2. Current Development Status

**Version 1.0: Initial Interactive Simulation**

The current implementation provides:

- Browser-based interactive simulation.
- Simplified two-dimensional incompressible stable-fluids solver.
- Predefined aerodynamic geometries.
- Custom geometry drawing and erasing.
- Angle-of-attack and model-size controls.
- Wind and environmental settings.
- Pressure and speed visualizations.
- Flow-particle trajectories.
- Approximate drag and lift estimates.
- Reynolds number and dynamic pressure calculations.
- Experimental vehicle-performance subsystem.
- Adaptive visualization quality settings.

The current version is an educational model, not a validated CFD application.

## 3. Development Philosophy

Future development will follow five principles.

### 3.1 Numerical Correctness Before Visual Complexity

Improvements to the numerical model should take priority over additional visual effects.

### 3.2 Reproducibility

Simulation conditions, configurations, and calculation methods should be documented so that results can be repeated and compared.

### 3.3 Transparent Limitations

Known numerical and physical limitations should remain visible in the documentation.

### 3.4 Incremental Engineering

Major improvements should be developed and tested in manageable stages rather than introduced as unverified changes.

### 3.5 Evidence-Based Validation

Claims of improved accuracy should be supported by numerical testing, appropriate benchmark comparisons, or experimental evidence.

## 4. Phase I: Numerical Foundations

<badge color="warning">High priority</badge> <badge>Planned</badge>

**Objective:** Improve understanding and control of the existing simulation model.

### Planned Work

- Investigate the pressure-correction procedure.
- Examine velocity divergence before and after pressure correction.
- Review inlet, outlet, wall, and obstacle boundary handling.
- Investigate numerical diffusion.
- Study the effect of vorticity confinement.
- Review numerical stability under different simulation conditions.
- Document the solver's mathematical assumptions more precisely.

### Expected Outcome

A better-understood numerical implementation with documented behaviour and more clearly identified sources of error.

## 5. Phase II: Physical Scaling and Grid Sensitivity

<badge color="warning">High priority</badge> <badge>Planned</badge>

**Objective:** Establish a more consistent relationship between physical reference quantities and numerical simulation parameters.

### Planned Work

- Investigate the relationship between physical airspeed and solver inlet velocity.
- Establish consistent grid-spacing and time-step interpretations.
- Review the treatment of viscosity and reference length.
- Investigate effective numerical Reynolds number.
- Perform grid-resolution sensitivity experiments.
- Compare results across progressively refined computational grids.
- Document the conditions under which numerical outputs change significantly.

### Expected Outcome

A more transparent physical-scaling framework and a documented understanding of grid-resolution dependence.

## 6. Phase III: Aerodynamic Force Estimation

<badge color="warning">High priority</badge> <badge>Planned</badge>

**Objective:** Improve the calculation and interpretation of aerodynamic force estimates.

### Planned Work

- Review pressure-based force estimation.
- Investigate integration over obstacle boundaries.
- Study the contribution of viscous shear.
- Review reference-area and reference-length definitions.
- Improve the consistency of drag and lift coefficient calculations.
- Investigate the sensitivity of force estimates to geometry rasterization.
- Compare calculated quantities against suitable analytical reference cases.

### Expected Outcome

More clearly defined aerodynamic estimates with documented assumptions and limitations.

## 7. Phase IV: Verification and Benchmark Evaluation

<badge color="warning">High priority</badge> <badge>Planned</badge>

**Objective:** Evaluate the numerical implementation against established reference problems.

### Planned Work

- Identify suitable publicly available benchmark geometries.
- Investigate simple analytical flow cases.
- Establish repeatable simulation configurations.
- Compare numerical outputs with reference results.
- Document discrepancies and possible sources of error.
- Investigate grid convergence where appropriate.
- Maintain a record of test conditions and results.

### Potential Evaluation Cases

- Uniform flow.
- Flow around a simple cylinder.
- Flow around a two-dimensional airfoil.
- Simplified channel-flow problems.
- Other suitable benchmark cases depending on the solver's supported physics.

### Expected Outcome

A documented verification and evaluation process.

Passing a numerical test or matching a particular reference case should not be treated as universal validation of the solver.

## 8. Phase V: Geometry and Visualization Improvements

<badge>Medium priority</badge> <badge>Planned</badge>

**Objective:** Improve geometry representation and the clarity of simulation outputs.

### Planned Work

- Investigate improved obstacle-boundary representation.
- Improve handling of curved geometries.
- Explore additional educational geometry presets.
- Provide clearer physical and normalized visualization scales.
- Improve comparisons between different simulation configurations.
- Distinguish dimensional quantities from normalized visualization values.
- Explore improved visualization of flow separation and vortical structures.

### Expected Outcome

A more informative and interpretable educational visualization environment.

## 9. Phase VI: Vehicle Performance Model

<badge>Medium priority</badge> <badge>Planned</badge>

**Objective:** Improve the structure and transparency of the experimental vehicle-performance subsystem.

### Planned Work

- Separate powertrain calculations from vehicle-motion calculations more clearly.
- Document engine and drivetrain assumptions.
- Review simplified turbocharger behaviour.
- Review NOS activation and power-delivery logic.
- Investigate more realistic rolling-resistance and aerodynamic-drag models.
- Improve the consistency of vehicle reference parameters.
- Explore more transparent relationships between simulated aerodynamic quantities and estimated vehicle performance.

### Expected Outcome

A better-documented educational vehicle-performance model.

A fully coupled physical vehicle-aerodynamics simulation is not assumed as part of the current implementation.

## 10. Phase VII: Performance and Architecture

<badge>Medium priority</badge> <badge>Planned</badge>

**Objective:** Improve maintainability and computational efficiency as the simulation develops.

### Planned Work

- Review numerical operations for optimization opportunities.
- Improve memory-management practices.
- Investigate Web Workers for computational workloads.
- Evaluate alternative browser-based rendering strategies.
- Improve separation between simulation, visualization, and interface logic.
- Investigate optional higher-resolution simulation configurations.

### Expected Outcome

A more maintainable and efficient browser-based architecture without sacrificing transparency or numerical testing.

## 11. Long-Term Research Directions

The following are exploratory directions rather than committed development milestones.

- More advanced numerical fluid-flow methods.
- Improved physical treatment of viscosity and turbulence.
- More sophisticated boundary-condition handling.
- Higher-resolution computational domains.
- Investigation of three-dimensional simulation approaches.
- Comparison against experimental wind-tunnel measurements.
- Educational tools for explaining numerical methods and aerodynamic assumptions.
- Reproducible benchmark and experiment configurations.

The feasibility of these directions will depend on technical requirements, available computational resources, and the results of earlier development phases.

## 12. Development Priority Summary

| Priority | Development area | Main objective |
|---|---|---|
| High | Numerical foundations | Understand and improve solver behaviour |
| High | Physical scaling | Establish consistent numerical and physical quantities |
| High | Grid sensitivity | Investigate resolution dependence |
| High | Force estimation | Improve aerodynamic calculation methodology |
| High | Verification | Establish repeatable benchmark evaluations |
| Medium | Geometry | Improve obstacle representation |
| Medium | Visualization | Improve interpretation and comparison |
| Medium | Vehicle model | Improve subsystem transparency |
| Medium | Architecture | Improve maintainability and performance |
| Exploratory | Advanced simulation | Investigate more sophisticated physical models |

## 13. Roadmap Policy

This roadmap is a development planning document.

- Priorities may change as technical investigations produce new findings.
- Planned work may be revised, postponed, or discontinued.
- A listed feature does not imply that implementation has started.
- A completed implementation does not automatically establish numerical correctness or physical validation.
- Any significant improvement in accuracy should be supported by appropriate documentation and testing.

Development progress should be reflected in the repository through updated documentation, version history, and reproducible evidence where applicable.

---

**Wind Tunnel Lab**  
An independent educational aerodynamics simulation project.

**Author:** Chitrarup Guha  
**Repository:** https://github.com/ChitrarupGuha/wind-tunnel-lab
