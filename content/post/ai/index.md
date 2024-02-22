+++
author = "Smbat Voskanyan"
title = "AI Algorithms Practice"
date = "2022-12-22"
description = "Writing N puzzle solution with AI in six different ways, with variations."
categories = [
    "AI"
]
tags = [
    "Java",
    "Algorithms"
]
image = "https://images.inc.com/uploaded_files/image/1920x1080/getty_484267200_109172.jpg"
+++

I took a bonus assignment for my Artificial Intelligence course. The work demonstrates the implementation of various algorithms for solving the n-puzzle problem, along with useful statistics for analysis. Due to the professor’s request, I have made the repository private, so students of upcoming years will not copy it, but you can access the code with **[this link](https://gitfront.io/r/SenPie/fhSwHm6Huxwx/ai-22/)**.

## Statistics
Part 1  
```
Executed Breadth First Tree Search
Nodes Generated 2298274; Max Nodes in frontier 1473871

Executed Breadth First Tree Search with Early Goal test
Nodes Generated 824404; Max Nodes in frontier 537119

Executed Breadth First Graph Search
Nodes Generated 5019; Max Nodes in frontier 1926

Executed Breadth First Graph Search with Early Goal test
Nodes Generated 4644; Max Nodes in frontier 1075

Skipped the execution of Depth First Tree Search
Algorithm gets into an infinite cycle of Right <-> Left actions 

Executed Depth First Graph Search
Nodes Generated 68217; Max Nodes in frontier 29633

Executed Iterative Deepening Tree Search
Nodes Generated 34232; Max Nodes in frontier 43
```
Both Breadth First Tree and Graph Searches found the optimal solution. Clearly huge improvements are observed with graph search version and the early goal test gives the extra bonus of cutting off extra nodes, that would be generated otherwise.   
Although, Depth First Tree Search is known to consume very little memory space it is not effective in this case as it gets into an infinite loop.  
Depth First Graph Search does a better job, than its Tree Search version xD. However, it generates many more nodes, than Breadth First Graph search and has a bigger frontier stretch.
Iterative Deepening Tree Search did a good job to find a solution, and it also spent very little memory. However, it is also worth to mention, that IDTS did not find the optimal solution. Also still, 4644 + 1075 < 34232 + 43 it still consumes more memory. You may argue, that compared to BFGS, IDTS does not use an extra set to keep track of _reached_ states, however reached states is not really making new states, but rather keeps references, which is still much less, than what we get with IDTS.   
Overall, Breadth First Graph Search with the early goal test comes out as a winner in uninformed search category, reason being, that it just works better for this problem.  
As it says in the book  
> When all step costs are equal, breadth-first search is optimal because it always expands the shallowest unexpanded node.


Part 2
```
Executed Uniform Cost Tree Search
Nodes Generated 2587508; Max Nodes in frontier 1653452

Executed Uniform Cost Graph Search
Nodes Generated 7549; Max Nodes in frontier 1656

Skipped the execution of Greedy Tree Search with h1 number of misplaced tiles
Algorithm gets into an infinite cycle.

Skipped the execution of Greedy Tree Search with h2 manhattan distance
Algorithm gets into an infinite cycle.

Executed Greedy Graph Search with h1 number of misplaced tiles
Nodes Generated 233; Max Nodes in frontier 68

Executed Greedy Graph Search with h2 manhattan distance
Nodes Generated 1051; Max Nodes in frontier 267

Executed A* Tree Search with h1, number of misplaced tiles Tree Search
Nodes Generated 964; Max Nodes in frontier 613

Executed A* Tree Search with h2 manhattan distance Tree Search
Nodes Generated 120; Max Nodes in frontier 74

Executed A* Graph Search with h1 number of misplaced tiles
Nodes Generated 360; Max Nodes in frontier 91

Executed A* Graph Search with h2 manhattan distance
Nodes Generated 106; Max Nodes in frontier 29
```
Before we continue any further, I would like to right away give the trophy to A* Graph Search with Manhattan Distance heuristic.  
Let's jump into it! Right away we can see that Uniform Cost Tree Search gave similar results to Breadth First Tree Search. Reason is that action cost is 1, and path costs gets incrementally bigger with each level forcing UCS to iterate in Breadth first manner. Reason why numbers are not same is connected to the fact how JDK implemented the PriorityQueue, which means it is not guaranteed to return the leftmost node in the same level.  
Same goes for Uniform Cost Graph Search and Breadth First Graph Search.  
Neither Number of Misplaced Tiles heuristic, nor Manhattan Distance heuristic are good enough on their own to run Tree Search, therefore Greedy Tree search gets into a cycle.
Again quoting the book:  
>Algorithms that don't remember the past are doomed to repeat the history.

Regarding A* Search we see power of good heuristic, because A* Tree Search with Manhattan distance performs better than A* Graph Search with Number of Misplaced Tiles heuristic. It is proved in the book that **h2** _dominates_ **h1**.  
It also has lower _Effective Branching Factor_.

| d   | BFS  | A*(h1) | A*(h2) |
|-----|------|--------|--------|
| 6   | 2.01 | 1.42   | 1.34   |
| 8   | 1.91 | 1.40   | 1.30   |
| 10  | 1.85 | 1.43   | 1.27   |
| 12  | 1.80 | 1.45   | 1.28   |
| 14  | 1.77 | 1.47   | 1.31   |
| 16  | 1.74 | 1.48   | 1.32   |
| 18  | 1.72 | 1.49   | 1.34   |
| 20  | 1.69 | 1.50   | 1.34   |
| 22  | 1.66 | 1.50   | 1.34   |
| 24  | 1.62 | 1.50   | 1.36   |


Overall, obviously and for the reasons mentioned before, A* Graph Search with Manhattan Distance heuristic comes top as a winner.

## Solution
Following is a demonstration of A* Graph Search on 8-puzzle with Manhattan Distance heuristics.
```
0: start

-------------
| 7 | 4 | 2 |
-------------
| 8 | 1 | 3 |
-------------
| 5 |   | 6 |
-------------

1: move LEFT

-------------
| 7 | 4 | 2 |
-------------
| 8 | 1 | 3 |
-------------
|   | 5 | 6 |
-------------

2: move UP

-------------
| 7 | 4 | 2 |
-------------
|   | 1 | 3 |
-------------
| 8 | 5 | 6 |
-------------

3: move UP

-------------
|   | 4 | 2 |
-------------
| 7 | 1 | 3 |
-------------
| 8 | 5 | 6 |
-------------

4: move RIGHT

-------------
| 4 |   | 2 |
-------------
| 7 | 1 | 3 |
-------------
| 8 | 5 | 6 |
-------------

5: move DOWN

-------------
| 4 | 1 | 2 |
-------------
| 7 |   | 3 |
-------------
| 8 | 5 | 6 |
-------------

6: move DOWN

-------------
| 4 | 1 | 2 |
-------------
| 7 | 5 | 3 |
-------------
| 8 |   | 6 |
-------------

7: move LEFT

-------------
| 4 | 1 | 2 |
-------------
| 7 | 5 | 3 |
-------------
|   | 8 | 6 |
-------------

8: move UP

-------------
| 4 | 1 | 2 |
-------------
|   | 5 | 3 |
-------------
| 7 | 8 | 6 |
-------------

9: move UP

-------------
|   | 1 | 2 |
-------------
| 4 | 5 | 3 |
-------------
| 7 | 8 | 6 |
-------------

10: move RIGHT

-------------
| 1 |   | 2 |
-------------
| 4 | 5 | 3 |
-------------
| 7 | 8 | 6 |
-------------

11: move RIGHT

-------------
| 1 | 2 |   |
-------------
| 4 | 5 | 3 |
-------------
| 7 | 8 | 6 |
-------------

12: move DOWN

-------------
| 1 | 2 | 3 |
-------------
| 4 | 5 |   |
-------------
| 7 | 8 | 6 |
-------------

13: move DOWN

-------------
| 1 | 2 | 3 |
-------------
| 4 | 5 | 6 |
-------------
| 7 | 8 |   |
-------------
```

{{< css.inline >}}
<style>
.canon { background: white; width: 100%; height: auto; }
</style>
{{< /css.inline >}}
