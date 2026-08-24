# AgiBot Raise A3 Ultra USD

[![USD](https://img.shields.io/badge/format-OpenUSD-7A4EAB)](https://openusd.org/)
[![Isaac Sim](https://img.shields.io/badge/Isaac%20Sim-6.0.1-76B900)](https://developer.nvidia.com/isaac/sim)
[![Asset Structure](https://img.shields.io/badge/Asset%20Structure-3.0-blue)](#asset-structure)

A simulation-ready USD asset for the AgiBot Raise A3 Ultra T3D0, designed for NVIDIA Isaac Sim 6.0.1 and organized according to Isaac Sim Asset Structure 3.0.

This repository includes the robot hierarchy, visual meshes, materials, colliders, mass and inertia properties, joint limits, and drive parameters. It also provides generic USD Physics, PhysX, and MuJoCo physics variants.

## Features

- Complete kinematic hierarchy for a bipedal humanoid robot
- Visual models, materials, and collision geometry
- Rigid-body mass, center of mass, and inertia properties
- Joint limits, maximum drive forces, and drive configurations
- Isaac Robot Schema support: `IsaacRobotAPI`, `IsaacLinkAPI`, `IsaacJointAPI`, and `IsaacSiteAPI`
- Selectable `Physics` Variant Set:
  - `none`: Loads no physics layer
  - `physics`: Loads engine-agnostic USD Physics configuration
  - `physx`: Loads PhysX-specific configuration; selected by default
  - `mujoco`: Loads the MuJoCo physics layer
- Metric units with Z as the up axis

## Compatibility

| Component | Version or Convention |
| --- | --- |
| NVIDIA Isaac Sim | 6.0.1 |
| Asset structure | Structure 3.0 |
| File format | OpenUSD (`.usd` / `.usda`) |
| Default Prim | `/agibot_a3` |
| Length unit | Meter |
| Up axis | Z |
| Default physics variant | `physx` |

> This asset is built for the schemas and asset structure used by Isaac Sim 6.0.1. Other versions and standalone OpenUSD tools may read the underlying USD content, but the behavior of Isaac- and PhysX-specific schemas may differ.

## Asset Structure

```text
raise_a3_ultra_t3d0/
├── interface.usda                 # Recommended Structure 3.0 entry point and Physics variants
├── raise_a3_ultra_t3d0.usda       # Compatibility entry point
└── payloads/
    ├── base.usda                  # Robot hierarchy and visual/collision instances
    ├── robot.usda                 # Isaac Robot Schema
    ├── geometries.usd             # Binary geometry data
    ├── instances.usda             # Reusable visual/collision instances
    ├── materials.usda             # Material definitions
    └── Physics/
        ├── physics.usda           # Engine-agnostic rigid-body, joint, and drive parameters
        ├── physx.usda             # PhysX-specific overrides
        └── mujoco.usda            # MuJoCo physics entry point
```

The asset is organized into layers using USD composition arcs:

1. `interface.usda` references `base.usda` to load the kinematic hierarchy and geometry instances.
2. `robot.usda` is added as a sublayer to provide Isaac Robot Schema metadata.
3. The `Physics` variant loads the corresponding physics layer as a payload when needed.
4. `base.usda` composes appearance and collision data from `materials.usda`, `instances.usda`, and `geometries.usd`.

## License

This project is licensed under the [Mulan Permissive Software License, Version 2 (Mulan PSL v2)](./LICENSE).
