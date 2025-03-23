# Parallel Picross Solver

## URL: 

## Summary:
We plan to implement the best parallel [picross](https://liouh.com/picross/) solver around the world. It will be balanced between efficiency (performance and scalability) and accuracy (making minimal mistakes during the attempts).


## Background:

A [Picross (Nonogram) puzzle](https://en.wikipedia.org/wiki/Picross) consists of a grid where cells must be either filled or empty based on numeric clues provided for each row and column. These clues specify the lengths and ordering of continuous blocks of filled cells within the corresponding rows or columns. Solving a Picross puzzle involves logical deduction, constraint propagation, and backtracking.

![Puzzle image](grid-shading-puzzle.jpg)

The solver uses an optimized backtracking algorithm enhanced with efficient constraint propagation techniques. To improve computational performance and scalability, we plan to parallelize it using shared-memory and distributed-memory (MPI) approaches. Shared-memory parallelism involves multiple threads accessing a shared representation of the puzzle grid concurrently, and it needs a lot of efforts on correctly using techniques we leanred in this class, such as **cache locality, locking vs lock free, atomic operations, memory consistency and cache coherence.**

On the other hand, we might MPI is utilized to partition the puzzle's workload across multiple processes. Each process independently handles subsets of rows or columns, propagating constraints locally and periodically synchronizing updates with other processes. As a result, there would be a lot of optimizaiton overhead on hanlding **workload imbalance, communication and synchronization overhead, messsage passing latency and different design strategies.**

Parallelism substantially benefits this solver by distributing constraint-checking tasks, speculative exploration of search branches, and conflict resolution across multiple cores or nodes. These parallelization strategies greatly reduce runtime, improve solver efficiency, and enable the handling of large Picross puzzles that would otherwise be computationally prohibitive.

## The Challenge:


Parallelizing a Picross solver is inherently challenging due to several key factors arising from the puzzle’s structure and constraints. The Picross puzzle involves interdependent constraints between rows and columns, meaning solving decisions made in one dimension directly impact the feasibility and options in the other. This interdependency introduces complex data dependencies, making parallel execution difficult since solving one constraint could invalidate assumptions made elsewhere in parallel.

### Workload:

The workload of a Picross solver involves extensive constraint propagation and search operations. While constraint propagation for rows and columns can initially be parallelized due to their independent structure at a coarse-grained level, synchronization points are required to merge state updates across threads or processes. This requirement can significantly reduce parallel efficiency due to synchronization overhead, leading to potential performance bottlenecks.

### Constraints:

Memory access characteristics also present challenges. Although there is some data locality (row and column states can be stored in contiguous memory for efficiency), the necessity for frequent synchronization and state merging between different solver units (threads or MPI processes) can result in high communication overhead relative to computation, particularly for larger grids. Communication overhead is exacerbated in distributed memory environments (MPI), where minimizing message passing is critical for performance.

Furthermore, execution divergence can occur during speculative backtracking phases, where different threads or processes explore alternative puzzle states. Some threads may quickly encounter contradictions, while others may continue exploration deeply into the search tree. This divergence can result in uneven workloads, inefficient resource utilization, and difficulties in maintaining balanced parallel performance.

System constraints further complicate workload mapping. Shared-memory systems must carefully manage concurrent updates to avoid race conditions without incurring significant synchronization overhead, typically through lock-free mechanisms or atomic operations. In distributed-memory systems (MPI), communication strategies must be carefully optimized to reduce latency and bandwidth usage, making efficient parallelization more challenging.

Through tackling these challenges, the project aims to gain deeper insights into managing complex dependencies, synchronization, and communication overhead effectively in parallel systems, leading to improved understanding of parallel algorithm design and performance optimization.

## Resources:

We will use GHC machines to test the scalability and performance from 1 thread to 8 threads. It would be really helpful if we could use PSC to test beyond 8 threads.


For Picross puzzle and solver details, we will implement it from scratch, but we will refer some of the following resources.
- [Backtracking Algorithm](https://en.wikipedia.org/wiki/Backtracking)
- [Slack overflow discussion](https://stackoverflow.com/questions/813366/solving-nonograms-picross)
- [Example1](https://github.com/rzippo/PicrossSolver?utm_source=chatgpt.com), [Example2](https://github.com/lukehutch/picross-solver?tab=readme-ov-file)

For the project idea and proposal, we refered another two game solvers in the previous semester:
- Parallel Conflict-Driven DPLL SAT solver for Killer Sudoku: https://github.com/liam-gersten/parallel-sat-solver/blob/main/writeups/project_proposal.md
- Wordle Solver and Evaluator: https://github.com/joel99/parallel_final/blob/main/static/proposal.md



## Goals and deliverables:

PLAN TO ACHIEVE:
- Having a good performance for solving [Picross puzzles](https://liouh.com/picross/) with matrix size from 5x5 to 30x30.
- Achieving a good optimization from baseline to our final version. [Someone](https://github.com/rzippo/PicrossSolver?utm_source=chatgpt.com) achieved 120x speedup.
- Maintaining a good scalability (possibly at least 3x-4x with 8 threads) and minimizing mistakes counts for the solver.

HOPE TO ACHIEVE:
- Achieving a really good scalability (6x-7x with 8 threads).
At Week 4:
    - If somehow successful, try to use another language and compare.
    - if really successful, try implementing Belief Propagation and compare.
    - if really really successful, try CUDA implementation and compare (CPU version with backtracking and recursion is really ineffcient and complicated on GPU).


## Platform Choice:

- We choose to use GHC machines for testing, and if we could have the access of PSC, it would be really helpful.
- We will use C++ which generally has the best performance. Since we used it for course projects, we are more familiar with those APIs.


## Schedule:

- Week 1: Baseline implementation
- Week 2: Parallelizing by shared memory model and OpenMP.
- Week 3: milestone report, Optimize and try MPI.
- Week 4: debug MPI and further optimization
    - If somehow successful, try to use another language and framework.
    - if really successful, try Belief Propagation
    - if really really successful, try CUDA implementation.
- Week 5: Writing up report and preparing poster.


