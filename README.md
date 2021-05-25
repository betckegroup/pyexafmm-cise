<h1 align='center'> PyExaFMM CiSE </h1>

# Outline

## 1 Introduction

### 1.1 Broad Strokes

- Particle FMM, why it's useful, and in which contexts.
- Current advances in written software for it
- Python, and it's utility.
- The concept of JIT and Numba, and how they work roughly.
- The point of this paper, why are we making another FMM? Tie together reasoning for using Python to code a non-trivial algorithm. (Ease of deployment, interoperbility with Python universe, low barrier to entry for non-software specialists)
- Can we code a HPC library using just Python data/numerics stack? If so it would make our lives as Computational Scientists a lot easier/faster! Allowing you to go from prototype to performance without software engineering hassle.
- Paper organisation in terms of following sections

### 1.2 Designing an FMM
- Basic concept behind KIFMM (relevant operations, and algorithm structure)
- Data structures required, morton representation, (linear) adaptive octree.
- Optimisations required for practical implementations, requirement to cache and store operators, quickly lookup (precomputed) operators, avoid redundant calculation (transfer vectors).
- Peculiarities of our FMM in order to achieve performance: rSVD compression of M2L, stability from ncheck_points > nequivalent_points.

### 1.3 Numba and Cupy
- Introduction to Numba, and how it can be useful for scientific computing - JIT compilation, interoperability with cupy/numpy data structures.
- How numba and cuda are used in this project, spell out where these technologies are actually impactful, and when they are not.
- Specifics of where they are used (AdaptOctree construction, M2L calculation/compression, P2P and P2M calculations)

## 2. Software Engineering

### 2.1 Software Design Principles:
- How much easier is it actually than just writing everything in C/C++?
- Was it easy to separate concerns, and enforce safety?
- How did the library design end up looking
- How did the code end up looking?
- Why is this important? Because these tools are only useful if they make our life easier and deployment of our ideas faster.

### 2.2 Software Design Specifics:
- How was code organised, and why. What bottlenecks did the design introduce on performance, if any (reliance on HDF5 for loading/caching operators).

## 3. Performance Comparison
- Accuracy, speed, and memory footprint as a function of experimental size. For different geometries. (See KIFMM Ying paper for some of the geometries that they try in that)
- Probably most important sections tbh...

## 4 Conclusion
- Still beaten by C++
- However, shows that we can code non-trivial algorithms fairly effectively in Python, but come with their own difficulties - programming to an invisible framework - and learning curve.
- Time wasted on (non-trivial) software issues to cope with/get around Python interpreter, could have been spent on optimising an already performant code.