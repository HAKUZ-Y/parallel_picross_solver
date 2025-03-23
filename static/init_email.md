title: Maggie/Youheng's 15-418/618 Project Discussion

Dear Prof. Mowry and Prof. Railing,

This is Maggie and Youheng and here is our ideas on the final project.
The detailed proposal draft is at https://github.com/HAKUZ-Y/parallel_picross_solver/blob/main/static/proposal.md.

We plan to parallelize the Picross Puzzle Solver. A Picross Puzzle consists of a grid where cells must be either filled or empty based on numeric clues provided for each row and column, and the idea is to optimize backtracking algorithm enhanced with efficient constraint propagation techniques.

We want to achieve a good balance between the efficiency (performance and scalability) and accuracy (making minimal mistakes during the attempts). The simple brute force version with sequential scanning might be simple to parallelize, which could provide us a baseline, but maintaining a low mistake counts needs each a lot of communication and synchronization overhead on each decisions, making it hard to achieve in parallel design.

We plan to implement C++ version and test in GHC machines. If we could have the access of PSC, it would be really helpful so that we can test the speed up beyond 8 threads.

PLAN TO ACHIEVE:
- Having a good performance for solving Picross puzzles with matrix size from 5x5 to 30x30.
- Achieving a good optimization from baseline to our final version. Someone achieved 120x speedup.
- Maintaining a good scalability (possibly at least 3x-4x with 8 threads) and minimizing mistakes counts for the solver.

HOPE TO ACHIEVE:
- Achieving a really good scalability (6x-7x with 8 threads). At Week 4:
    - If somehow successful, try to use another language and compare.
    - If really successful, try implementing Belief Propagation and compare.
    - If really really successful, try CUDA implementation and compare (CPU version with backtracking and recursion is really ineffcient and complicated on GPU).


Best Regrads,
Maggie Gong & Youheng Yang