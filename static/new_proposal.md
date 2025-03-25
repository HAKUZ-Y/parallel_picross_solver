

Hi Prof. Mowry and Prof. Railing,

Our original project idea was creating a puzzle solver, which might not be a great fit, so we started exploring new ideas after the discussion this morning. Here is a very brief overview of the 2 new ideas we currently have in mind, and we'd really appreciate it if you could take a look over them and provide us some feedback before proceeding to the actual proposal.

**First Idea - Parallel discrete wavelet transform**
Wavelet transform is a algorithm used for signal and image processing by decomposing a signal into components at different frequency bands.



**Challenges:**
Workload Imbalance: 
- Early levels contain more data and work than later levels, leading to imbalance between threads/processors as levels progress. Some processes might finish early, and we need to work on dynamic load balancing.

Data dependency: 
- There is a data dependency across level since each level depends on the results of the previous one, so synchronization will be needed before proceeding to the next level of computation.

Dynamic Data Movement: 
- We might also want to work on multi-dimensional transforms, where values may move between processors, and memory access can be irregular.

To make it more challenging, we could work on a streaming version instead of processing a static image / signal. In this case data is processed in real-time as it arrives, and we have to figure out overlapping computation with data movement.

---------
**Second Idea - Parallel PageRank Algorithm with streaming input:**


To mock real time application, we plan to parallelize the pagerank algorithm with streaming input, which means after each iteration, some nodes will be added and dropped.

**Challenges:**
Workload Imbalance: 
- Skewed degree distributions lead to uneven computation

Dynamic Data Movement: 	
- Cross-node rank updates require non-local access

Synchronization Overhead: 
- Iteration barriers limit speedup

Data Dependency: 
- PageRank at t+1 depends on in-links' values at t

The main computation task:
![alt text](image.png)