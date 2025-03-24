title: Maggie/Youheng's 15-418/618 Project Discussion

Dear Prof. Mowry and Prof. Railing,

This is Maggie and Youheng and here is our ideas on the final project. The detailed proposal draft is at https://github.com/HAKUZ-Y/parallel_picross_solver/blob/main/static/proposal.md.

We plan to parallelize the Picross Puzzle Solver. A Picross game involves solving Nonogram puzzles, which consists of a grid with numeric clues defined for every row and column. Those numbers define the cells that must be filled in consecutively for that row / column, but the positions of those that must be left empty are not specified in the clues. 

We plan to start with implementing a backtracking algorithm and optimize it along the way with efficient constraint propagation techniques. Due to the nature of this puzzle game, the time required to find a solution is expected to grow exponentially with the puzzle size. Our goal is to achieve a good balance between the efficiency (performance and scalability) and accuracy (making minimal mistakes during the attempts).

The simple brute force version with sequential scanning might be straightforward to parallelize, which could provide us a baseline. However, the challenge lies in maintaining a low mistake counts while ensuring all row and column constraints are satisfied. Since solving such puzzles requires exploring many configurations, a parallel implementation would introduce a lot of communication and synchronization overhead on each decisions, making it hard to achieve in a parallel design.

We plan to implement C++ version and test in GHC machines. If we could have the access of PSC, it would be really helpful so that we can test the speed up beyond 8 threads.

**PLAN TO ACHIEVE:**
- Having a good performance for solving Picross puzzles with matrix size from 5x5 to 30x30.
- Achieving a good optimization from baseline to our final version by exploring both shared memory and MPI approaches. We aim to approach achieved speedups by multiple orders of magnitude.
- Maintaining a good scalability (possibly at least 3x-4x with 8 threads) and minimizing mistakes counts for the solver.

**HOPE TO ACHIEVE:**
- Achieving a really good scalability (6x-7x with 8 threads). At Week 4:
    - If somehow successful, try to use another language, compare and analyze the results.
    - If really successful, try implementing Belief Propagation message passing algorithm, compare and analyze the results
    - If really really successful, try CUDA implementation and compare (CPU version with backtracking and recursion is really inefficient and complicated on GPU).
    
Best Regards, Maggie Gong & Youheng Yang
