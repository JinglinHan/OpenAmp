# OpenCircuit

This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.

***

OpenCircuit is an open-source data set of 10k behaviourial-level three-stage operational amplifiers (opamps). Each circuit has distinct design, and the netlist, device parameters and simulated performance of each circuit are provided. 

The netlist is given in 

> /circuit_10k/{id}/circuit/netlist.

In 

> /circuit_10k/{id}/tmp.conf 

 we give the list of all design parameters corresponding to the netlist along with their available ranges.

The final design parameters after tuning is given in 

> /circuit_10k/{id}/output

where the final FoM is also included.

The simulation results can be found in 

> /circuit_10k/{id}/sim.out

which is derived with Cadence Spectre. The three numbers are DC gain (dB), phase margin (degree) and GBW (GHz), respectively. If less than three numbers are shown in the sim.out file, it's because the gain is a less-than-zero value and no valid phase margin and GBW result can be computed. If so, the FoM is set to 0.

The circuit design is also given in form of graph adjacency matrix. The definition of the graph and its adjacency matrix can be found in our paper. In short, the graph nodes represent the circuit nodes and the edges represent different devices.

| Edge weight | Device                                 |
| :---------: | -------------------------------------- |
|      0      | not connect                            |
|      1      | Resister                               |
|      2      | Capacitor                              |
|      3      | Parallel resister and capcitor         |
|      4      | Serial resister and capacitor          |
|      5      | Feedforward +gm                        |
|      6      | Feedforward -gm                        |
|      7      | Serial resister and feedforward +gm    |
|      8      | Serial capacitor and feedforward +gm   |
|      9      | Serial resister and feedforward -gm    |
|     10      | Serial capacitor and feedforward -gm   |
|     11      | Parallel resister and feedforward +gm  |
|     12      | Parallel capacitor and feedforward +gm |
|     13      | Parallel resister and feedforward -gm  |
|     14      | Parallel capacitor and feedforward -gm |
|     15      | Feedback +gm                           |
|     16      | Feedback -gm                           |
|     17      | Parallel resistor and feedback +gm     |
|     18      | Serial resistor and feedback +gm       |
|     19      | Parallel capacitor and feedback +gm    |
|     20      | Serial capacitor and feedback +gm      |
|     21      | Parallel resistor and feedback -gm     |
|     22      | Serial resistor and feedback -gm       |
|     23      | Parallel capacitor and feedback -gm    |
|     24      | Serial capacitor and feedback -gm      |

The adjacency matrix is given in
> /circuit_10k_clean/{id}/vec.csv

with the following intepretation.

| 0    | 0    | {4}  | {5}  | 0    |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 5    | {1}  | {2}  |
| {4}  | 5    | 0    | 6    | {3}  |
| {5}  | {1}  | 6    | 0    | 5    |
| 0    | {2}  | {3}  | 5    | 0    |

Most elements in the adjacency matrix are fixed so that the generated circuit is likely to be valid. The {1} to {5} in the matrix should be replaced by the 1st to 5th number in 
> /circuit_10k/{id}/vec.csv,

and the result is the adjacency matrix of that circuit.

The 10k designs are randomly generated based on the code of https://github.com/jialinlu/OPAMP-Generator.


In
> /circuit_10k.csv

you can find the vertorized adjacency matrix of each circuit and its simulation results. This summary might be more friendly to parse.

Have fun :）



_The authers appreciate Dr. Jialin Lu for his contribution to open-source EDA community and for giving us the insights on topology generation._

_The authors also appreciate Dr. Ming Cheng for all the constructive discussions with us._

***

## Reference

J. Han, Y. Leng, X. Zhang and P. Wang, "TSO-Flow: A Topology Synthesis and Optimization Workflow for Operational Amplifiers with Invertible Graph Generative Model", _2024 ACM/IEEE International Conference on Computer-Aided Design (ICCAD), New Jersey, USA._

