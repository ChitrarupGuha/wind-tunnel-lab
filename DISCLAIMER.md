# Disclaimer

**Project:** Wind Tunnel Lab  
**Last updated:** 7 November 2026

## 1. Educational Purpose

Wind Tunnel Lab is an independent, browser-based educational project developed to demonstrate and explore fundamental concepts of aerodynamics and fluid flow.

The project is intended for educational use, personal experimentation, demonstration, and learning. It provides a simplified environment in which users can interact with geometries, visualize airflow-related fields, and explore approximate aerodynamic quantities.

It is not intended to replace professional computational fluid dynamics (CFD) software, laboratory experiments, engineering analysis, or qualified professional judgment.

## 2. Simplified Simulation Model

The current implementation uses a simplified two-dimensional incompressible stable-fluids solver.

The simulation makes assumptions and simplifications to keep the model interactive and computationally manageable in a web browser. Real-world aerodynamic behaviour is considerably more complex and may involve three-dimensional effects, compressibility, turbulence, heat transfer, complex boundary conditions, and other physical phenomena that are not fully represented by this implementation.

Consequently, visualizations and numerical outputs should be interpreted as educational approximations rather than exact representations of physical airflow.

## 3. Accuracy of Results and Numerical Outputs

Wind Tunnel Lab may display or calculate quantities including, but not limited to:

- Airflow velocity and pressure visualizations.
- Flow-particle trajectories.
- Approximate drag and lift forces.
- Approximate drag coefficient (Cd) and lift coefficient (Cl).
- Reynolds number and dynamic pressure.
- Other derived or simulated aerodynamic values.

These outputs are dependent on the simulator's implementation, numerical resolution, geometry, boundary conditions, configuration, and simplifying assumptions.

Changes in simulation settings or grid resolution may produce materially different results. Numerical outputs may contain errors, instability, discretization effects, or other inaccuracies.

**No displayed value should be assumed to be experimentally measured, scientifically validated, or suitable for direct comparison with real-world engineering data unless independently verified.**

## 4. No CFD or Experimental Validation Claim

Wind Tunnel Lab is not currently presented as a validated computational fluid dynamics solution.

Unless explicitly documented otherwise for a particular version or test case:

- The solver has not been established as experimentally validated.
- Its results have not been demonstrated to agree with accepted CFD benchmark datasets.
- Its aerodynamic coefficients and force estimates should not be treated as authoritative engineering measurements.
- Visual similarity to real airflow does not establish numerical accuracy.

Any future validation claims must be supported by documented methodology, appropriate reference cases, and reproducible comparisons.

## 5. Not for Safety-Critical or Professional Engineering Decisions

Do not use Wind Tunnel Lab as the sole basis for:

- Aircraft, spacecraft, or aviation design.
- Road vehicle, racing vehicle, or other transport design.
- Structural or mechanical engineering decisions.
- Safety-critical system design or operation.
- Manufacturing specifications or product certification.
- Regulatory compliance or engineering approval.
- Any decision where inaccurate aerodynamic information could cause injury, property damage, financial loss, or other harm.

Real-world engineering applications require appropriate analytical methods, qualified professional review, and, where necessary, validated CFD simulations or physical testing.

Users are responsible for independently verifying any information or conclusions derived from the project before applying them outside an educational environment.

## 6. No Warranty

Wind Tunnel Lab is provided on an **"AS IS"** and **"AS AVAILABLE"** basis, subject to the terms of its applicable licence.

To the maximum extent permitted by applicable law, the project author makes no express or implied warranty regarding:

- Accuracy, correctness, or completeness of simulation results.
- Reliability or consistency of numerical outputs.
- Fitness for a particular purpose.
- Suitability for professional or commercial engineering use.
- Continuous availability or uninterrupted operation.
- Compatibility with every browser, device, or environment.
- Absence of software defects, errors, or unexpected behaviour.

The project may contain bugs, incomplete features, numerical limitations, or implementation errors.

## 7. Limitation of Liability

To the maximum extent permitted by applicable law, the project author shall not be responsible for losses, damages, claims, or liabilities arising from the use of, inability to use, or reliance upon Wind Tunnel Lab or its outputs.

This includes, without limitation, direct or indirect losses, property damage, financial loss, business interruption, or consequences resulting from engineering decisions based on unverified simulation results.

Nothing in this disclaimer excludes or limits any liability that cannot legally be excluded or limited under applicable law.

## 8. Independent Project and Institutional Affiliation

Wind Tunnel Lab is an independently developed project.

Unless explicitly stated in a separate written authorization, the project is not affiliated with, sponsored by, approved by, or endorsed by any university, research institution, laboratory, company, or government organization.

References to academic institutions, researchers, facilities, publications, or external resources do not imply their participation in, approval of, or validation of this project.

## 9. External References and Third-Party Materials

The project may refer to external publications, datasets, tools, libraries, or educational resources.

Such references are provided for informational or development purposes. Their inclusion does not imply endorsement, and their respective owners retain their applicable rights.

Users are responsible for reviewing and complying with the terms and conditions governing any third-party resources they access or use.

## 10. Updates and Maintenance

The project may be modified, updated, expanded, restricted, or discontinued at the author's discretion.

There is no guarantee of future updates, maintenance, technical support, feature availability, or backward compatibility.

A feature, calculation, or visualization available in one version may behave differently or become unavailable in a later version.

## 11. Relationship with the Project Licence

This disclaimer describes the intended use, technical limitations, and risks associated with Wind Tunnel Lab.

It does not grant additional permissions to copy, modify, distribute, host, sell, sublicense, or commercially exploit the project.

Use, redistribution, modification, and commercial permissions are governed by the project's applicable `LICENSE` file or a separate written agreement where applicable.

If a separate written commercial agreement governs a particular use, its terms apply to that use. Nothing in this disclaimer is intended to override rights or obligations that cannot legally be waived.

## 12. Acceptance of Responsibility

By using Wind Tunnel Lab, you acknowledge that:

1. The simulator is an educational approximation, not a validated engineering tool.
2. Its numerical outputs may be inaccurate or incomplete.
3. You will independently assess the suitability of any results before relying on them.
4. You will not treat its outputs as a substitute for qualified engineering analysis, validated simulation, or physical testing.
5. You are responsible for how you use, interpret, and apply the information generated by the project.

If you do not agree with these conditions, discontinue use of the project.

---

**Wind Tunnel Lab**  
An independent educational aerodynamics simulation project.

**Source code:** https://github.com/ChitrarupGuha/wind-tunnel-lab
