---
title: Mixed State Entanglement In Quantized Chaotic Systems
project_type : thesis
permalink: /research/quantum-chaos
date: 2016-06-15
excerpt : Master's thesis carried out at IIT Madras. We study the connections between chaos and quantum entanglement. We study entanglement in mixed states of quantized chaotic systems, focusing on the quantum coupled standard map.<br><center><img src="https://adi3e08.github.io/files/research/ddp/chaos.png" width="45%"/></center>'
author_profile: False
---
<p align="center">
<img src="https://adi3e08.github.io/files/research/ddp/chaos.png" width="60%"/>
</p>

This work represents my master's thesis carried out at IIT Madras, with [Prof. Arul Lakshminarayan](https://sites.google.com/view/arulakshminarayan){:target="_blank"}. We studied the connections between chaos and quantum entanglement. We studied entanglement in mixed states of quantized chaotic systems, focusing on the quantum coupled standard map. We explored entanglement dynamics with varied interaction strengths and environment dimensions. We identified a critical dimension where entanglement decreases, potentially posing challenges in contexts like quantum computing.

You can view my complete thesis [here](https://drive.google.com/file/d/1Shu4J47R_wIqWh6opb5N7-mZth3mWA3c/view){:target="_blank"}.

## Summary
Many physical systems in nature, for example, all atoms and molecules except the hydrogen atom (and related two-body atomic systems) exhibit chaos when treated classically [[1]](#1) [[2]](#2). The same atoms and molecules when treated quantum mechanically, exhibit quantum chaos [[3]](#3). Decoherence, which explains wavefunction collapse as the quantum nature of a system "leaks" into it's environment, is strongly influenced by chaos in the system / environment [[4]](#4). Also, quantum chaos is known to have an important place in the foundation of quantum statistical mechanics [[5]](#5). Thus, the study of quantum chaos becomes important from a general quantum mechanical perspective.  

Quantum entanglement is a physical phenomenon where, many particles interact in ways such that, given a quantum state for the system as a whole, each particle cannot be assigned a single state vector [[6]](#6). Entanglement has been part of the foundational discussions of quantum mechanics since the time of Schrodinger [[7]](#7) (who gave it it's name) and the famous EPR paper of Einstein, Podolski and Rosen [[8]](#8). Entanglement is a topic of extensive contemporary research due to it's newly found applications to quantum information and quantum computation [[6]](#6).

Quantum chaos is known to impact entanglement in a non trivial manner [[9]](#9). Whether it will potentially aid or hinder a quantum computer remains unanswered. Almost all previous work on entanglement in quantized chaotic systems have dealt only with pure states, either stationary states (eigenstates) or other time evolved non-stationary pure states. In reality, even a carefully prepared and isolated system tends to interact with its environment, which has the effect of leaving the system in a mixed state. Thus, the study of mixed state entanglement in quantized chaotic systems forms an important and unexplored problem and forms the focus of this study.

We consider a prototypical system, the standard map [[10]](#10) [[11]](#11), which is essentially a periodically kicked pendulum. It is a simple system that exhibits classical chaos for certain values of its parameters. We let two standard maps interact through a potential to obtain a coupled standard map. We then quantize the coupled standard map to obtain the quantum coupled standard map, which is our system of interest. We study its entanglement under time evolution for initial states that are mixed, for different interaction strengths between the standard maps and different dimensions of the surrounding environment. We find that, for a given interaction strength, as we increase the environment dimension, the tendency to get entangled reduces and there exists a critical dimension in most cases, beyond which the state remains separable at all times. Such a phenomenon is potentially a problem in situations where entanglement is desirable, such as in quantum computing.

<!-- As a preliminary, Chapter 2 discusses kicked Hamiltonian systems, whose classical maps are developed. In particular, a well studied model system, the standard map [[11]](#11) [[12]](#12) which is a periodically kicked pendulum is discussed and it's classical dynamics studied. The classical map is then quantized to obtain a quantum map, the Quantum Standard Map, which allows us to study Quantum Chaos rather easily [[13]](#13). It's eigenstates are computed and their spread in phase space is studied through the Husimi represenation. The nearest neighbour spacing distribution(NNSD), which measures how the spacing between nearest eigenangles are distributed is also computed. Both the eigenstate plots and NNSD are seen to be influenced by the classical dynamics of the classical standard map. 

Chapter 3 discusses bipartite systems in general, defines important concepts such as density matrix, entanglement and presents entanglement measures for pure and mixed states.

Chapter 4 presents our bipartite system of interest, the coupled standard map, which consists of two interacting standard maps. It is first quantized to obtain the quantum coupled standard map. It's NNSD and also the entanglement of it's stationary states (eigenstates) are computed. This part of the thesis reproduced earlier work and benchmarked the numerical algorithms used.

The remaining portion of the thesis, presents the original work done. The variation of average stationary state entanglement with interaction strength (between the standard maps) is studied for different standard map parameters and compared with a previous work [[14]](#14) which derived an approximation for the same under certain assumptions on the parameters. We look at how the approximation holds in situations where the assumptions are not true. Next, time evolution of the system for different initial conditons is studied, and entanglement monitored so as to understand the general entangling behaviour of the system. 

The remaining portion of the thesis, presents the main problem of interest to this study. We investigate mixed state entanglement of quantized chaotic systems. We study the quantum coupled standard map $AB$ under time evolution for an initial mixed state of the form $\rho_{AB}(0)=\rho_{A}(0) \otimes \rho_{B}(0)$, where $\rho_{A}(0)$ and $\rho_{B}(0)$ are obtained by tracing out the environments $C$ and $D$ from random pure states $\rho_{AC}(0)$ and $\rho_{BD}(0)$ respectively. The study is performed for different interaction strengths between the standard maps and different dimensions of the environment. -->

## References
<a id="1">[1]</a>
Blümel, R., & Reinhardt, W. P. (1997). Chaos in atomic physics (No. 10). Cambridge University Press.

<a id="2">[2]</a>
Gutzwiller, M. C. (2013). Chaos in classical and quantum mechanics (Vol. 1). Springer Science & Business Media.

<a id="3">[3]</a>
Porter, M. A. (2001). An introduction to quantum chaos. arXiv preprint nlin/0107039.

<a id="4">[4]</a>
Zurek, W. H., & Paz, J. P. (1994). Decoherence, chaos, and the second law. Physical Review Letters, 72(16), 2508.

<a id="5">[5]</a>
Srednicki, M. (1994). Does quantum chaos explain quantum statistical mechanics?. arXiv preprint cond-mat/9410046.

<a id="6">[6]</a>
Horodecki, R., Horodecki, P., Horodecki, M., & Horodecki, K. (2009). Quantum entanglement. Reviews of modern physics, 81(2), 865.

<a id="7">[7]</a>
Schrödinger, E. (1935, October). Discussion of probability relations between separated systems. In Mathematical Proceedings of the Cambridge Philosophical Society (Vol. 31, No. 4, pp. 555-563). Cambridge University Press.

<a id="8">[8]</a>
Einstein, A., Podolsky, B., & Rosen, N. (1935). Can quantum-mechanical description of physical reality be considered complete?. Physical review, 47(10), 777.


<a id="9">[9]</a>
Lakshminarayan, A. (2001). Entangling power of quantized chaotic systems. Physical Review E, 64(3), 036207.

<a id="10">[10]</a>
Chririkov, B. V. (1979). A universal instability of many-dimensional oscillators systems. Phys Rep, 52, 265.

<a id="11">[11]</a> 
Lichtenberg, A. J., & Lieberman, M. A. (2013). Regular and chaotic dynamics (Vol. 38). Springer Science & Business Media.

<!-- <a id="13">[13]</a> 
F. M. Izrailev.
Simple models of quantum chaos: spectrum and eigenfunctions. 2003.

<a id="14">[14]</a> 
Arul Lakshminarayan and others.
Entanglement and localization transitions in eigenstates of interacting chaotic systems. 2016. -->
