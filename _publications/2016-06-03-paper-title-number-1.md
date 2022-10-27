---
title: "Mixed State Entanglement In Quantized Chaotic Systems"
permalink: /publications/dual-degree-project
excerpt : 'This work represents my masters thesis carried out at IIT Madras. We study the connections between chaos and quantum entanglement. In particular, we study mixed state entanglement in quantized chaotic systems, which forms an important and unexplored problem, with possible implications for quantum computing.'
---
<!-- date : 2016-06-03 -->
This work represents my master's thesis carried out at IIT Madras. I worked with [Prof. Arul Lakshminarayan](https://sites.google.com/view/arulakshminarayan){:target="_blank"}.

You can view my complete thesis [here](https://drive.google.com/file/d/1Shu4J47R_wIqWh6opb5N7-mZth3mWA3c/view){:target="_blank"}.

# Summary
Many physical systems in nature, for example, all atoms and molecules except the hydrogen atom (and related two-body atomic systems) exhibit chaos when treated classically [[1]](#1) [[2]](#2). The quantization of classically chaotic systems is one of the most frequently studied forms of quantum chaos [[3]](#3). This means that the same atoms and molecules, when treated quantum mechanically would exhibit quantum chaos. Decoherence, which explains wavefunction collapse as the quantum nature of a system "leaks" into it's environment, is strongly influenced by chaos in the system/environment [[4]](#4). Also, quantum chaos is known to have an important place in the foundation of quantum statistical mechanics [[5]](#5). Thus, the study of quantum chaos becomes important from a general quantum mechanical perspective.  

Quantum entanglement is a physical phenomenon that occurs when many particles interact in ways such that given a quantum state for the system as a whole, each particle cannot be assigned a single state vector [[6]](#6). Entanglement has been part of the foundational discussions of quantum mechanics since the time of Schrodinger [[7]](#7) (who gave it it's name) and the famous EPR paper of Einstein, Podolski and Rosen [[8]](#8). Entanglement is a topic of extensive contemporary research due to it's newly found applications to quantum information and quantum computation [[9]](#9).

Quantum chaos is known to impact entanglement in a non trivial manner [[10]](#10). Whether it will potentially aid or hinder a quantum computer remains unanswered. Almost all previous work on entanglement in quantized chaotic systems have dealt only with pure states, either stationary states (eigenstates) or other time evolved non-stationary pure states. In reality even a carefully prepared and isolated system tends to interact with it's environment, which has the effect of leaving the system in a mixed state. Thus, the study of mixed state entanglement in quantized chaotic systems forms an important and unexplored problem and forms the focus of this study. 

As a preliminary, Chapter 2 discusses kicked Hamiltonian systems, whose classical maps are developed. In particular, a well studied model system, the standard map [[11]](#11) [[12]](#12) which is a periodically kicked pendulum is discussed and it's classical dynamics studied. The classical map is then quantized to obtain a quantum map, the Quantum Standard Map, which allows us to study Quantum Chaos rather easily [[13]](#13). It's eigenstates are computed and their spread in phase space is studied through the Husimi represenation. The nearest neighbour spacing distribution(NNSD), which measures how the spacing between nearest eigenangles are distributed is also computed. Both the eigenstate plots and NNSD are seen to be influenced by the classical dynamics of the classical standard map. 

Chapter 3 discusses bipartite systems in general, defines important concepts such as density matrix, entanglement and presents entanglement measures for pure and mixed states.

Chapter 4 presents our bipartite system of interest, the coupled standard map, which consists of two interacting standard maps. It is first quantized to obtain the quantum coupled standard map. It's NNSD and also the entanglement of it's stationary states (eigenstates) are computed. This part of the thesis reproduced earlier work and benchmarked the numerical algorithms used.

The remaining portion of the thesis, presents the original work done. The variation of average stationary state entanglement with interaction strength (between the standard maps) is studied for different standard map parameters and compared with a previous work [[14]](#14) which derived an approximation for the same under certain assumptions on the parameters. We look at how the approximation holds in situations where the assumptions are not true. Next, time evolution of the system for different initial conditons is studied, and entanglement monitored so as to understand the general entangling behaviour of the system. 

The remaining portion of the thesis, presents the main problem of interest to this study. We investigate mixed state entanglement of quantized chaotic systems. In particular, the quantum coupled standard map $AB$ is studied under time evolution for an initial mixed state of the form $\rho_{AB}(0)=\rho_{A}(0) \otimes \rho_{B}(0)$, where $\rho_{A}(0)$ and $\rho_{B}(0)$ are obtained by tracing out the environments $C$ and $D$ from random pure states $\rho_{AC}(0)$ and $\rho_{BD}(0)$ respectively. The study is performed for different sets of interaction strength $b$ and Environment Dimension $D_{E}$ and the results are recorded.

### References
<a id="1">[1]</a>
R. Blumel and W. P. Reinhardt.
Chaos in Atomic Physics. 1997.

<a id="2">[2]</a>
Martin C. Gutzwiller.
Chaos  in  Classical  and  Quantum  Mechanics. 1997.

<a id="3">[3]</a>
Mason A. Porter.
An Introduction to Quantum Chaos. 2001.

<a id="4">[4]</a>
Wojciech Hubert Zurek and Juan Pablo Paz.
Decoherence, Chaos, and the second law. 1994.

<a id="5">[5]</a>
Mark Srednicki.
Does quantum chaos explain quantum statistical mechanics ? 1995.

<a id="6">[6]</a>
Ryszard Horodecki and others.
Quantum entanglement. 2007.

<a id="7">[7]</a>
E. Schrodinger.
Proc. Camb. Philos. Soc. 31, 555. 1935.

<a id="8">[8]</a>
A. Einstein, B. Podolski, N. Rosen.
Can Quantum-Mechanical Description of Reality Be Considered Complete ? 1935.

<a id="9">[9]</a>
Horodecki, Ryszard and others.
Quantum entanglement. 2009.

<a id="10">[10]</a>
Arul Lakshminarayan.
Entangling power of quantized chaotic systems. 2000.

<a id="11">[11]</a>
B . V. Chririkov.
A universal instability of many-dimensional oscillator systems. 1979.

<a id="12">[12]</a> 
Lichtenberg, A.J. and Lieberman, M.A.
Regular and Chaotic Dynamics. 1992.

<a id="13">[13]</a> 
F. M. Izrailev.
Simple models of quantum chaos: spectrum and eigenfunctions. 2003.

<a id="14">[14]</a> 
Arul Lakshminarayan and others.
Entanglement and localization transitions in eigenstates of interacting chaotic systems. 2016.
