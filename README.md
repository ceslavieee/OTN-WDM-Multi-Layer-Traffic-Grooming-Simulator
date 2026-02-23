、# OTN-WDM Multi-Layer Traffic Grooming Simulator

## Project Overview
This repository contains a Python-based simulation environment designed to solve the **Optimal Intermediate Grooming Point** problem in optical networks. Traffic grooming allows for the transmission of multiple low-rate services (10G/100G) using a single high-capacity optical lightpath, which saves spectrum and reduces the number of costly optical transponders.

The goal of this project is to propose a heuristic that maximizes network capacity while minimizing the number of established lightpaths by strategically selecting grooming nodes.



## Core Concepts
* **Intermediate Grooming**: Instead of creating end-to-end tunnels for every service, services can be "groomed" (aggregated) at intermediate nodes to fill high-capacity wavelengths.
* **Multilayer Routing**: The simulator considers both OTN (Layer 1) and WDM (Layer 0) constraints simultaneously.
* **Constraint-Based Simulation**: Each node has a finite capacity based on physical hardware limitations.

## Technical Specifications & Constraints
The simulation strictly adheres to the following OTN switch parameters:

| Parameter | Constraint Value |
| :--- | :--- |
| **Maximum ODU frames** | 100 ODUs (10G and 100G) |
| **Total Switching Capacity** | 12 Tb/s |
| **I/O Card Slots** | 70 ports (for I/O cards and transponders) |
| **I/O Card Capacity** | 100 Gb/s (supports 10x10G or 1x100G) |
| **WDM Lightpath Capacity** | 100 Gb/s to 500 Gb/s per wavelength |



## File Descriptions
* `OTH_en.py`: **The Resource Engine.** Models the physical hardware (OTN1/OTN2 classes). It calculates I/O card usage, switching matrix load, and total capacity consumption.
* `R_en.py`: **The Simulation Driver.** Generates random traffic, implements k-path routing (k=3), and compares "Grooming" vs "No-Grooming" scenarios.

## Simulation Workflow
1.  **Topology Generation**: Creates a network graph (default 100 nodes).
2.  **Service Generation**: Generates random 10G/100G services between random source-destination pairs.
3.  **Path Selection**: Evaluates up to 3 possible paths per service to find a valid route that satisfies all hardware constraints.
4.  **Iterative Loading**: Starts with a base load and increments until the **blocking rate reaches 1%**.
5.  **Data Analysis**: Outputs the number of WDMs used and the total savings ratio achieved through grooming.

## How to Run
### Prerequisites
* Python 3.x
* Dependencies: `networkx`, `matplotlib`, `numpy`

### Execution
Run the main simulation script to generate performance plots:
```bash
python R_en.py
