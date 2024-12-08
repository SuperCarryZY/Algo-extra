# CMPS 6610 Extra Credit Answers
  
In this extra credit assignment, we will test and review concepts you
   have learned since the midterm exam. Please add your written answers
   to `answers.md` which you can convert to a PDF using
   `convert.sh`. Alternatively, you may scan and upload written
   answers to a file named `answers.pdf`.



1. **Algorithmic Paradigms**

- 1a. 
The brute-force method for solving the unit-weight task scheduling problem involves trying all possible subsets of tasks to find the best schedule. For  n  tasks, there are  2^n  subsets. For each subset, you check if the tasks can be scheduled without missing their deadlines. This involves sorting the subset (which takes  O(nlogn)  in the worst case) and verifying its feasibility.

The work is  O(2^n*nlogn) , as you need to process  2^n  subsets, each requiring sorting and verification. The span is  O(nlog n) , because the checks for different subsets can happen in parallel, and the longest sequential step is sorting and validating one subset.

While this approach is simple, its exponential work makes it impractical for large  n . It’s mainly useful for small-scale problems or as a baseline for comparison with more efficient algorithms, like greedy or dynamic programming methods.
- 1b.
  No.
  Suppose we have the following tasks  (start, end, weight) :
	1.	Task A:  (1, 3, 10) 
	2.	Task B:  (2, 5, 20) 
	3.	Task C:  (4, 6, 30)
Greedy Algorithm:
Sorted tasks: A ( 1 to 3, 10 ), B ( 2 to 5, 20 ), C ( 4 to 6, 30 ). Pick Task A ( weight = 10 ).Next, pick Task C ( weight = 30 ) since it does not overlap with A. Total weight =  10 + 30 = 40 .Optimal Solution: Instead, choose Task B ( 2 \to 5, 20 ) and Task C ( 4 \to 6, 30 ).The greedy algorithm misses this optimal solution.

Total weight =  20 + 30 = 50 .

- 1c.
The weighted task scheduling problem can be solved using dynamic programming because it has an optimal substructure property. This means that the best solution for scheduling tasks up to a certain point can be determined by deciding whether to include the current task in the schedule. If we include it, we add its weight to the best solution of all tasks that don’t overlap with it. If we exclude it, we simply use the solution without this task. This choice ensures that we systematically find the best possible schedule.

To implement this, tasks are sorted by their end times, and for each task, we determine the latest task that doesn’t conflict with it. The optimal weight for the entire schedule is then calculated step by step, either including or excluding each task based on which gives the higher total weight

The algorithm’s work is  O(nlog n) , mainly due to sorting tasks and finding overlaps using binary search. The span, which reflects the longest sequential operations, is also  O(nlog n) . This approach balances efficiency with thoroughness, making it suitable for solving weighted scheduling problems.

2. **Graphs**

- 2a. 
BFS works well for finding the shortest path in an unweighted graph because it assumes all edges have the smae or weight. It explores nodes layer by layer, guaranteeing that the first time it reaches a node, it has found the shortest path. However, in a weighted graph, edges can have different weights, and the shortest path might involve fewer total weights but more edges. BFS does not account for this and can lead to incorrect results.

Imagine a graph with the following edges and weights:A - B  with weight 1  A - C  with weight 10 B - C  with weight 1

The goal is to find the shortest path from  A  to  C . Using BFS, the algorithm starts at  A  and visits all its neighbors. It first explores  A \to B , then directly explores  A to C , assigning a path weight of 10 to  C . BFS stops here, believing  A to C  is the shortest path because it does not consider the weights of edges.

However, the correct shortest path is  A to B to C , which has a total weight of  1 + 1 = 2 . BFS fails because it assumes all edges have the same weight and prioritizes paths based on the number of edges, not their cumulative cost.

In weighted graphs, BFS is inadequate as it ignores edge weights. Algorithms like Dijkstra’s prioritize paths based on cumulative weights, ensuring the shortest path is found even when weights vary.


- 2b. 
The Bellman-Ford and Dijkstra algorithms both solve the shortest path problem but are designed for different scenarios.

Bellman-Ford is more versatile because it works for graphs with negative edge weights and can even detect negative weight cycles. It calculates the shortest paths by repeatedly relaxing all edges up to  V-1  times, where  V  is the number of vertices. However, it’s slower, with a time complexity of O(VE) , which makes it less efficient for large graphs, especially dense ones.
Dijkstra, on the other hand, is faster for graphs with non-negative weights. By using a priority queue, it selects the next closest vertex efficiently, with a time complexity of  O(V + Elog V) . However, it fails for graphs with negative weights and doesn’t detect negative weight cycles.

- 2c. 
The cycle property for minimum spanning trees states that in any graph containing a cycle, the edge with the largest weight in that cycle cannot be part of the MST. This can be explained as follows:
A minimum spanning tree is defined as a subset of edges that connects all vertices without forming cycles, while minimizing the total weight of the edges. If a cycle exists in the graph, it means there are multiple paths connecting the same vertices. In such cases, removing any edge from the cycle does not disconnect the graph.
To prove the property, consider a cycle in the graph and focus on its largest weight edge. If this edge is included in the spanning tree, it is possible to remove it and replace it with a lighter edge from the same cycle while keeping the graph connected. This replacement reduces the total weight of the tree, contradicting the assumption that the tree was already a minimum spanning tree.
Thus, the largest weight edge in a cycle is always excluded from the MST to ensure the tree has the minimum possible weight. This is why the cycle property holds true for any graph.

3. **Randomization**

![IMG_500A1FAA01D5-1](https://github.com/user-attachments/assets/e3652c23-7bfd-429c-86b6-39e03b071478)

- 5a. 
