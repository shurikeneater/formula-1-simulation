# Idea: F1 Vehicle Physics Simulation — Planning Brief

**Role:** Senior Vehicle Dynamics Engineer & Scientific Software Architect

You are an expert in Formula 1 vehicle dynamics, motorsport engineering, computational physics, numerical simulation, Python scientific computing, and software architecture.

Your task is to create a comprehensive, technically rigorous, implementation-ready `PLAN.md` for an Advanced Formula 1 Vehicle Physics Simulation project.

Do not write the actual application code yet. Your primary deliverable is a complete engineering and development roadmap that another AI coding agent or software engineering team can follow step by step.

---

## 1. Project Overview

**Project name:** F1 Vehicle Physics Simulation

**Objective:** Build a high-fidelity Formula 1-inspired vehicle physics simulation using Python.

The simulator should mathematically model the physical behavior of a racing vehicle, including:

- Vehicle dynamics
- Aerodynamics
- Tire dynamics
- Suspension systems
- Powertrain
- Braking systems
- Weight transfer
- Steering and cornering
- Thermal behavior
- Vehicle stability

The ultimate goal is to create a modular, extensible simulation capable of reproducing realistic racing vehicle behavior and comparing simulation results against available real-world telemetry data.

> **Important:** Do not claim the simulator is an exact reproduction of a modern F1 car. Use publicly available information, documented engineering principles, and clearly identified assumptions.

## 2. Technical Stack

- **Primary programming language:** Python 3.11+
- **Scientific computing:** NumPy, SciPy, Pandas
- **Visualization:** Matplotlib, Plotly
- **Development and testing:** pytest, Pydantic, Jupyter Notebook, Git
- **Optional future extensions:**
  - PyVista or Blender for 3D visualization
  - CasADi for optimization
  - Simulink interoperability
  - FastF1 for historical telemetry acquisition

Choose stable and compatible versions when implementation begins.

## 3. System Architecture

Design a modular architecture with the following components.

### A. Vehicle Dynamics

Implement:

- Longitudinal dynamics
- Lateral dynamics
- Vertical dynamics
- Yaw dynamics
- Pitch dynamics
- Roll dynamics
- Vehicle coordinate systems
- Center of gravity
- Weight distribution
- Load transfer

Evaluate whether a 3-DOF bicycle model, 7-DOF model, or 14-DOF model is appropriate for each development stage. Explain the mathematical assumptions and limitations of each model.

### B. Aerodynamics

Implement:

- Aerodynamic drag
- Downforce generation
- Front and rear aerodynamic balance
- Ride-height sensitivity
- Speed-dependent aerodynamic forces
- Air density effects
- Wind effects
- Ground effect approximation

Include equations such as:

- Drag force: $F_d = \tfrac{1}{2} \rho C_d A v^2$
- Downforce: $F_{down} = \tfrac{1}{2} \rho C_l A v^2$

Explain aerodynamic coefficients, reference area, sign conventions, and limitations.

### C. Tire Dynamics

Implement progressively:

- Basic friction model
- Longitudinal tire force
- Lateral tire force
- Slip ratio
- Slip angle
- Load sensitivity
- Combined slip
- Tire temperature effects
- Tire degradation approximation

Evaluate the use of the Pacejka Magic Formula. Explain the parameters required and identify which values need calibration.

### D. Suspension System

Implement:

- Spring stiffness
- Damper coefficients
- Suspension travel
- Wheel loads
- Heave motion
- Pitch motion
- Roll motion
- Anti-roll bars
- Ride height
- Aerodynamic interaction

Define the equations of motion and explain the required parameters.

### E. Powertrain

Implement:

- Engine power curve
- Engine torque curve
- RPM
- Gear ratios
- Gear shifting
- Differential behavior
- Drivetrain efficiency
- Traction limits
- Power-dependent acceleration

Use a simplified powertrain model initially and explain how to improve it.

### F. Braking System

Implement:

- Brake force
- Brake bias
- Brake torque
- Tire-limited braking
- Weight transfer under braking
- ABS-free racing brake model
- Brake temperature approximation

### G. Thermal Model

Implement optional progressive models for:

- Tire temperature
- Brake temperature
- Engine temperature
- Cooling effects
- Thermal degradation

Clearly distinguish simplified approximations from experimentally validated models.

## 4. Initial Vehicle Parameters

Create a configurable vehicle parameter system. Use the following provisional starting values for the first prototype:

| Parameter                 | Value | Unit          |
| ------------------------- | ----- | ------------- |
| Vehicle mass              | 800   | kg            |
| Frontal area              | 1.5   | m²            |
| Air density               | 1.225 | kg/m³         |
| Drag coefficient          | 0.9   | dimensionless |
| Downforce coefficient     | 3.0   | dimensionless |
| Wheelbase                 | 3.6   | m             |
| CG height                 | 0.30  | m             |
| Tire friction coefficient | 1.7   | dimensionless |
| Maximum engine power      | 750   | kW            |

> These are prototype assumptions, **NOT** verified specifications of a real F1 car.

The architecture must allow every parameter to be modified through configuration files. Include:

- `car_parameters.yaml`
- `tire_parameters.yaml`
- `aero_parameters.yaml`
- `suspension_parameters.yaml`
- `powertrain_parameters.yaml`

Explain parameter units, valid ranges, default values, and uncertainty.

## 5. Numerical Simulation Engine

Design a reliable numerical simulation framework. Cover:

- Simulation time step
- Numerical integration
- Initial conditions
- State variables
- System inputs
- ODE formulation
- Solver selection
- Stability
- Numerical error
- Event detection
- Simulation termination conditions

Evaluate:

- Explicit Euler
- Semi-implicit Euler
- Runge-Kutta 4
- SciPy `solve_ivp`

Explain when each method should be used. The simulation engine must support reproducible runs and configurable simulation settings.

## 6. Track Model

Design a track representation system. Support:

- Track centerline
- Track curvature
- Track elevation
- Track width
- Corner sections
- Straight sections
- Track distance
- Coordinate transformations

Start with a simplified track model, then design a pathway toward importing real circuit geometry. Do not assume that telemetry alone provides complete track geometry.

## 7. Data Acquisition and Calibration

Research and document possible data sources:

- FastF1
- Jolpica F1 API
- Kaggle Formula 1 datasets
- Public motorsport engineering research
- Publicly available vehicle dynamics datasets

For each source explain:

- Available data
- Data format
- Access method
- Limitations
- Licensing considerations
- Whether it contains actual vehicle physics parameters

Design a calibration framework for:

- Aerodynamic coefficients
- Tire parameters
- Vehicle mass
- Powertrain characteristics
- Braking behavior

Do not invent missing physical parameters. Use configurable assumptions with confidence labels:

- Measured
- Publicly documented
- Estimated
- Assumed

Explain how to compare simulated lap behavior with available telemetry.

## 8. Project Directory Structure

Design a scalable project directory structure. Consider:

```
f1_vehicle_sim/
├── PLAN.md
├── README.md
├── pyproject.toml
├── configs/
├── data/
├── docs/
├── notebooks/
├── src/
│   └── f1sim/
│       ├── core/
│       ├── vehicle/
│       ├── aerodynamics/
│       ├── tires/
│       ├── suspension/
│       ├── powertrain/
│       ├── brakes/
│       ├── thermal/
│       ├── track/
│       ├── simulation/
│       ├── calibration/
│       ├── visualization/
│       └── utils/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── validation/
├── scripts/
└── results/
```

You may improve this structure if necessary. Explain the responsibility of every major directory and module.

## 9. Development Roadmap

Divide the project into clear phases:

1. Project setup and physical foundations
2. Basic vehicle dynamics
3. Aerodynamic modeling
4. Tire modeling
5. Suspension modeling
6. Powertrain and braking
7. Integrated vehicle dynamics
8. Track simulation
9. Telemetry integration and calibration
10. Visualization and analysis
11. Validation and optimization

For each phase specify:

- Objectives
- Tasks
- Required mathematical knowledge
- Required data
- Expected output
- Dependencies
- Unit tests
- Acceptance criteria
- Potential difficulties

Define clear milestones and measurable completion criteria.

## 10. Testing and Validation

Design a serious engineering testing framework. Include:

- Unit tests for every physics module
- Integration tests
- Numerical stability tests
- Dimensional consistency tests
- Energy consistency checks
- Boundary condition tests
- Parameter sensitivity tests
- Regression tests
- Comparison with analytical solutions
- Comparison with available real telemetry

Explain how to distinguish software correctness from physical model accuracy. Do not claim physical validation without supporting data.

## 11. Visualization and Outputs

The system should eventually generate:

- Vehicle speed vs time
- Acceleration vs time
- Longitudinal and lateral acceleration
- Aerodynamic drag vs speed
- Downforce vs speed
- Tire force graphs
- Tire slip angle graphs
- Suspension displacement
- Wheel load distribution
- Yaw rate
- Roll and pitch
- Brake force
- Engine power and torque
- Track trajectory

Plan an interactive visualization dashboard as an optional future extension.

## 12. Engineering Documentation

The `PLAN.md` must include:

- Executive summary
- Project goals
- Scope and non-goals
- System architecture
- Physics modules
- Mathematical models
- Parameter definitions and units
- Data acquisition strategy
- Numerical methods
- Software architecture
- Directory structure
- Development phases
- Testing strategy
- Validation methodology
- Performance considerations
- Risks and limitations
- Future extensions
- Glossary
- References and further reading
- Final project acceptance criteria

For every major physics subsystem include:

- Physical explanation
- Governing equations
- Variables and units
- Assumptions
- Required parameters
- Input/output interfaces
- Implementation dependencies
- Validation approach

## 13. Engineering Quality Requirements

Follow these principles:

- SI units throughout the simulation.
- Explicit coordinate conventions.
- Consistent sign conventions.
- Modular architecture.
- Type hints.
- Documented public interfaces.
- Reproducible numerical experiments.
- Configurable parameters.
- Separation of physics from visualization.
- Separation of raw data from calibrated parameters.
- No hardcoded undocumented physical constants.
- No arbitrary parameter values presented as real F1 specifications.

Avoid unnecessary complexity in the first prototype. Build a physically meaningful minimum viable simulator first, then progressively increase fidelity.

## 14. Expected Deliverable

Create a complete `PLAN.md` file in the project root. The document must be detailed enough that an AI coding agent can implement the project phase by phase without having to invent the architecture.

Use:

- Clear Markdown headings
- Mathematical equations in LaTeX
- Tables for parameters
- Mermaid diagrams for architecture and dependencies
- Checklists for milestones
- Explicit implementation priorities

Write the documentation in professional technical English. Do not implement application code yet.

Before finalizing, check that:

- [ ] All physics modules are covered.
- [ ] All equations define their variables and units.
- [ ] All dependencies are explained.
- [ ] All project phases have acceptance criteria.
- [ ] All assumptions are identified.
- [ ] The roadmap is technically coherent.
- [ ] The document is internally consistent.

The final action should be to save the complete document as `PLAN.md` in the project root.
