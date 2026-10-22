# Dynamo
## A Primary Visual Cortex Inspired Neural Network Accelerator Framework

A PIM accelerator framework for continuous-coupled neural networks (CCNNs), with a neighborhood-coupled dataflow also applicable to pulse-coupled neural networks (PCNNs).

**Status:** This work is currently get a major revision at **ACM Transactions on Architecture and Code Optimization (TACO)**. Stay tuned for updates!

## Highlights

- **Dynamics–hardware co-design:** We propose Dynamo to accelerate the nonlinear dynamics of CCNNs through coordinated model simplification, execution control, and dataflow design.
- **Hardware-friendly computation:** CHASE replaces exponential operators and sigmoid functions with shifts and piecewise-linear approximations while retaining the nonlinear dynamics needed by the evaluated workloads.
- **History-gated execution:** A dual-mode execution unit detects periodic behavior or a configured chaotic-mode stopping condition to skip low-return iterations, reducing the average iteration count by approximately **70%**.
- **Local neighborhood communication:** An HBM-PIM-inspired architecture keeps neuron states and eight-neighbor communication local, reducing data movement during iterative execution.
- **Efficiency and fidelity:** The synthesized prototype achieves **972.80 GOP/s** and **1,660.07 GOP/s/W** on the native **16 × 16 CCNN tile workload**, with high output similarity to the original CCNN. Additional PCNN experiments evaluate the applicability of the neighborhood-coupled dataflow.

## Motivation

CCNNs model complex nonlinear dynamics inspired by the primary visual cortex, but their execution on conventional hardware is expensive. Three challenges motivate Dynamo:

- Exponential and sigmoid operations increase the cost of repeated neuron updates.
- Fixed iteration budgets continue computation after outputs reach useful dynamical regimes.
- Frequent accesses to neighboring neuron outputs introduce communication overhead.

Dynamo addresses these challenges using hardware-friendly approximations, history-gated execution, and a dataflow designed for neighborhood coupling.
![Motivation](https://github.com/user-attachments/assets/827353b6-51b5-48e3-9c17-0e9f27b6d03c)


## Overall Architecture

![Overall Architecture](https://github.com/user-attachments/assets/632c1ad6-1191-4456-a901-2cbf6bb55476)

Dynamo consists of three main components:

1. **CHASE — CCNN Hardware-friendly Approximation and Simplification for Efficient Inference:** simplifies costly nonlinear operations into hardware-friendly arithmetic.
2. **Dual-mode history-gated execution unit:** uses neuron output history to identify stopping conditions and avoid unnecessary subsequent updates.
3. **Neighborhood-coupled dataflow:** maps coupled neurons to processing elements and supports local exchange of neighboring outputs.

The architecture follows an **HBM-PIM design paradigm**. The evaluated synthesized prototype contains **2 × 2 macroblocks with 256 processing elements**, corresponding to a native **16 × 16 neuron array**.

## Abstract

Continuous-coupled neural networks provide a detailed model of nonlinear dynamics inspired by the primary visual cortex, supporting visual signal processing and brain simulation. However, costly nonlinear operations, repeated iterations, and frequent neighborhood communication make conventional hardware execution inefficient. We propose Dynamo, a dynamics–hardware co-design accelerator framework that combines CHASE, a dual-mode history-gated execution unit, and a neighborhood-coupled dataflow. CHASE replaces hardware-unfriendly exponential and sigmoid operations with shifts and piecewise-linear functions. History-gated execution skips low-return iterations using output-history-based stopping conditions. The neighborhood-coupled dataflow reduces communication overhead by keeping iterative neuron interactions local. Experiments on CBIS-DDSM and VIPL-HR show approximately 70% fewer iterations with high output similarity to the original CCNN. Native-cluster evaluation reports 972.80 GOP/s and 1,660.07 GOP/s/W, with energy-efficiency gains of approximately 948× over an Intel Core i9 CPU and 1,537× over an NVIDIA RTX 6000 GPU on the evaluated workload.

## Results

### Native CCNN Cluster

The following results are reported for the **16 × 16 CCNN tile workload**. Dynamo hardware results are based on a **synthesized 45 nm prototype evaluated at 200 MHz**.

| Metric | Dynamo |
| --- | ---: |
| Processing elements | 256 |
| Throughput | 972.80 GOP/s |
| Power | 0.586 W |
| Energy efficiency | 1,660.07 GOP/s/W |
| Energy-efficiency gain over Intel Core i9 | Approximately 948× |
| Energy-efficiency gain over NVIDIA RTX 6000 | Approximately 1,537× |

### Iteration Reduction and Output Fidelity

SSIM measures similarity between Dynamo outputs and the original CCNN outputs.

| Dataset | Average iterations | Iteration reduction | SSIM |
| --- | ---: | ---: | ---: |
| CBIS-DDSM | 8.99 | 70.03% | 0.989 |
| VIPL-HR | 8.92 | 70.26% | 0.997 |

The paper also evaluates PCNN on CBIS-DDSM to test the applicability of Dynamo's neighborhood-coupled dataflow to another coupled neural model.

## Code Availability

Code and reproduction instructions will be added to this repository.

## Installation

Dependency and toolchain requirements will be provided with the code release.

## Quick Start

Commands for running the experiments will be provided with the code release.

## Citation

Citation information will be added when public bibliographic details become available.

