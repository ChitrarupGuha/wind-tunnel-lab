# Wind Tunnel Lab

**An interactive, browser-based 2D aerodynamic visualization and educational simulation environment.**

Wind Tunnel Lab is an experimental project exploring how airflow visualization, geometry interaction, and simplified vehicle-performance modelling can make aerodynamic concepts more accessible.

The project runs directly in a modern web browser without requiring a separate installation.

## Current Features

- Interactive airflow visualization.
- Pressure and velocity-field visualization.
- Particle-based airflow trails.
- Preset geometries: car, bike, plane, wing, Laval nozzle, and blank canvas.
- Freehand geometry drawing and erasing.
- Adjustable geometry angle and size.
- Adjustable tunnel airflow and vortex intensity.
- Adaptive rendering quality.
- Experimental vehicle-performance model with throttle, gears, turbo boost, and nitrous oxide simulation.

## Technology

- HTML5
- CSS3
- JavaScript
- HTML Canvas API

## Getting Started

1. Clone this repository:

   ```bash
   git clone https://github.com/YOUR-USERNAME/wind-tunnel-lab.git
   ```

2. Open the project directory.

3. Run `index.html` in a modern web browser.

No build system or package installation is currently required.

## Project Status

**Experimental prototype / active development**

The current implementation uses a simplified 2D velocity-field simulation and approximate aerodynamic calculations.

It is intended for educational exploration and interactive visualization. It is not a validated computational fluid dynamics (CFD) solver and should not be used for professional engineering design, safety-critical decisions, or experimental certification.

## Known Limitations

- The simulation is two-dimensional and does not represent full 3D airflow.
- Aerodynamic coefficients and forces are estimates, not experimentally validated measurements.
- The current solver has not yet been validated against established experimental benchmark datasets.
- The vehicle-performance model is simplified and is not a physically complete powertrain model.
- Results may vary with geometry, simulation settings, and numerical approximations.

## Development Roadmap

- [ ] Separate wind-tunnel and vehicle-driving simulation modes.
- [ ] Improve solver formulation and numerical stability.
- [ ] Introduce configurable physical parameters.
- [ ] Improve aerodynamic force and coefficient calculations.
- [ ] Add Reynolds number and pressure coefficient visualization.
- [ ] Add experiment saving and A/B geometry comparison.
- [ ] Introduce benchmark-based verification and validation.
- [ ] Improve mobile and accessibility support.
- [ ] Develop an educational learning module.

## Scientific Integrity

The project aims to distinguish visualization from physical prediction.

Any future numerical improvements will be documented alongside their assumptions, limitations, and validation status.

## Contributions and Feedback

Technical feedback, educational suggestions, bug reports, and discussions about aerodynamic modelling are welcome.

If you are an aerospace engineering student, researcher, or developer interested in educational simulation tools, feel free to explore the project and share your feedback.

## Disclaimer

This is an independent educational software project. It is not affiliated with, endorsed by, or validated by any university, research institution, or wind-tunnel facility.

---

**Developed by Chitrarup Guha**
