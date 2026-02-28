# Developing a Fundamental Diagram for Urban Air Mobility Traffic Based on Physical Experiments

## Overview

This repository provides the data and (forthcoming) source code associated with the following paper:

> **Zhou, H., Zhai, Y., Shen, S., Ouyang, Y., Shi, X., and Li, X. (2025).** 
> Developing a Fundamental Diagram for Urban Air Mobility Based on Physical Experiments. *arXiv preprint arXiv:2512.21425*.

[[2512.21425\] Developing a Fundamental Diagram for Urban Air Mobility Traffic Based on Physical Experiments](https://arxiv.org/abs/2512.21425)

Urban Air Mobility (UAM) leverages unmanned aerial vehicles to reduce travel time and alleviate congestion in urban environments. As drone density increases, UAM traffic exhibits congestion phenomena analogous to those observed in ground transportation systems.

This repository supports the proposed methodology in the paper, including:
- generation of simulation-based UAM trajectories,
- execution of reduced-scale physical experiments using Bitcraze Crazyflie drones, and
- construction of fundamental diagrams (FDs) for UAM traffic.

In addition, we release a trajectory-based UAM traffic flow dataset, **UAMTra2Flow**, derived from both simulation and physical experiments.



https://github.com/user-attachments/assets/c91ed3dd-3e1a-46ca-8b2a-afa451e7482c



## Repository Layout

```
.
├── simulation_trajs/      # Simulation trajectory dataset
├── field_test_trajs/      # Physical experiment trajectories
└── README.md              # Documentation
```

## Installation

If you plan to run the source code (to be released), please prepare a Python 3 environment and install the required dependencies once they are provided. The physical experiment platform runs on an Ubuntu system with the hardware and software configuration described in the paper.

### Hardware

The physical experiments in this study are conducted using **Bitcraze Crazyflie 2.1+** nano quadrotors. Each Crazyflie has a compact footprint (approximately 10 cm × 10 cm) and supports precise onboard control and external positioning, making it well suited for reduced-scale UAM traffic experiments.

For localization, we employ the **Bitcraze Lighthouse v2** positioning system. 4 Lighthouse base stations are deployed to provide high-precision indoor positioning within the experimental airspace, enabling accurate trajectory recording and repeatable traffic experiments.

### Software

All physical experiments are orchestrated using **Crazyswarm2**, an open-source multi-robot control framework built on ROS 2. Crazyswarm2 provides high-level APIs for trajectory execution, swarm coordination, and data logging, and serves as the core software interface between the Crazyflie drones and the Lighthouse positioning system.

## Usage

### Code

The source code will be released upon acceptance of the paper.

### Data

All datasets are provided in CSV format.

#### Simulation data

```
simulation_trajs/
  Sx_Cy_Hz/
    Sx_Cy_Hz_Dn_m.csv
```

#### Field test data

```
field_test_trajs/
  Sx_Cy_Hz/
    Sx_Cy_Hz_Dn.csv
    Sx_Cy_Hz_Dn/
      Sx_Cy_Hz_Dn_cfXX.csv
```

#### Naming convention

- `S1 / S2 / S3` → scenario type: random / alternating / fixed stations  
- `C1 / C2` → control strategy: stop-and-yield / circular-detour  
- `Hz` → safety spacing of *z* meters (e.g., `H0.6` indicates 0.6 m)  
- `Dn` → number of drones (e.g., `D6` indicates 6 drones)  
- `m` → simulation run index (1, 2, ...)  
- `cfXX` → Crazyflie ID / per-drone log index  

For field experiments, `Sx_Cy_Hz_Dn.csv` contains the merged trajectories of all drones in a given experiment, while files under `Sx_Cy_Hz_Dn/` store per-drone logs.

**Note:** Both simulation trajectories and merged field-test trajectories exclude takeoff and landing phases.

#### Data attributes

| Column Name | Description                         | Unit |
|------------|-------------------------------------|------|
| id         | Drone ID                            | N/A  |
| time       | Timestamp (Δt = 0.1 s)              | s    |
| px         | x-coordinate of drone position      | m    |
| py         | y-coordinate of drone position      | m    |
| pz         | z-coordinate of drone position      | m    |
| dest_px   | x-coordinate of current destination | m    |
| dest_py   | y-coordinate of current destination | m    |
| dest_pz   | z-coordinate of current destination | m    |

During takeoff and landing phases, the values of `dest_px`, `dest_py`, and `dest_pz` are set to 0.

## Developers

**Developers:** Hang Zhou (hzhou364@wisc.edu), Yuhui Zhai (yuhui3@illinois.edu), Shiyu Shen (sshen10@illinois.edu)

For questions or feedback, please contact the **CATS Lab** at the University of Wisconsin–Madison.
