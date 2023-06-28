# Maximum probability of successfully reaching the ending node

## Problem:

You are given a directed graph with `n` nodes, numbered from `0` to `n-1`. The graph is represented by an array of edges, where `edges[i] = [u, v]` denotes a directed edge from node `u` to node `v`. Each edge also has an associated probability `succProb[i]`, which represents the probability of successfully traversing the edge.

You are also given a starting node `start` and an ending node `end`. Your goal is to find the maximum probability of successfully reaching the ending node `end` starting from the starting node `start`.

Write a function `double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end)` that returns the maximum probability. If it is impossible to reach the ending node, return `0.0`.

**Function Signature:**

```cpp
double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end)
```

**Input:**

* `n` (1 <= n <= 10^4): An integer representing the number of nodes in the graph.
* `edges`: A 2D vector of integers representing the directed edges in the graph. Each entry `edges[i] = [u, v]` indicates a directed edge from node `u` to node `v`. It is guaranteed that there are no self-loops (edges where `u = v`) and at most one directed edge between any pair of nodes.
* `succProb`: A vector of doubles representing the probabilities of successfully traversing the corresponding edges in `edges`. Each `succProb[i]` (0 <= succProb\[i] <= 1) represents the probability of successfully traversing the edge `edges[i]`.
* `start` (0 <= start < n): An integer representing the starting node.
* `end` (0 <= end < n): An integer representing the ending node.

**Output:**

* Return the maximum probability of successfully reaching the ending node `end` starting from the starting node `start`. If it is impossible to reach the ending node, return `0.0`.

**Note:**

* The answer will be considered correct if the absolute difference between the returned value and the actual answer is at most 1e-5.
* It is guaranteed that there exists at least one path from the starting node to the ending node.

## Solution:

```cpp
#include <vector>
#include <queue>
#include <iostream>
#include <limits>

using namespace std;

class Solution {
public:
    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end) {
        vector<vector<pair<int, double>>> graph(n);
        for (int i = 0; i < edges.size(); i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            double p = succProb[i];
            graph[u].push_back({v, p});
            graph[v].push_back({u, p});
        }
        
        vector<double> maxProb(n, 0.0);
        maxProb[start] = 1.0;
        
        priority_queue<pair<double, int>> pq;
        pq.push({1.0, start});
        
        while (!pq.empty()) {
            double curProb = pq.top().first;
            int curNode = pq.top().second;
            pq.pop();
            
            if (curProb < maxProb[curNode]) {
                continue;
            }
            
            for (const auto& neighbor : graph[curNode]) {
                int nextNode = neighbor.first;
                double nextProb = curProb * neighbor.second;
                
                if (nextProb > maxProb[nextNode]) {
                    maxProb[nextNode] = nextProb;
                    pq.push({nextProb, nextNode});
                }
            }
        }
        
        return maxProb[end];
    }
};

```

Let's go through the code and explain the coding pattern step by step:

1. The `maxProbability` function takes the number of nodes `n`, a 2D vector `edges` representing the edges between nodes, a vector `succProb` representing the edge probabilities, the starting node `start`, and the ending node `end`. It returns the maximum probability of reaching the end node from the start node.
2. First, the code constructs a graph representation using an adjacency list. It iterates through the `edges` vector and adds the edges along with their probabilities to the `graph` vector of vectors.
3. Next, a `maxProb` vector is created to store the maximum probabilities for each node. Initially, all elements in `maxProb` are set to 0.0, except for the starting node `start`, which is set to 1.0 since the probability of reaching the starting node is 1.
4. The code uses a priority queue (`pq`) to implement a modified version of Dijkstra's algorithm. The priority queue stores pairs of probabilities and nodes, prioritizing the nodes with higher probabilities. It starts with the starting node and its probability 1.0.
5. The main part of the algorithm begins with a while loop that continues until the priority queue (`pq`) becomes empty.
6. Inside the loop, the code extracts the node with the highest probability (`curNode`) from the priority queue along with its corresponding probability (`curProb`).
7. It then checks if the extracted probability (`curProb`) is less than the maximum probability recorded for the current node (`curNode`). If so, it means that a shorter or higher probability path has already been found, so it continues to the next iteration of the while loop.
8. For each neighbor of the current node, the code calculates the probability of reaching that neighbor (`nextNode`) from the current node by multiplying the current probability (`curProb`) with the probability of the edge connecting them.
9. If the calculated probability (`nextProb`) is greater than the maximum probability recorded for the neighbor node (`maxProb[nextNode]`), it means a higher probability path has been found. The `maxProb[nextNode]` is updated with `nextProb`, and the neighbor node is added to the priority queue (`pq`) with its corresponding probability `nextProb`.
10. Once the while loop finishes, the maximum probability of reaching the end node (`maxProb[end]`) is returned.

Overall, the code follows a modified Dijkstra's algorithm to find the maximum probability of reaching the end node from the start node. It utilizes a priority queue to explore the nodes with higher probabilities first, updating the maximum probabilities as it traverses the graph.

## Example:

\
Let's go through an example to understand how the code works.

Let's say we have the following inputs:

* `n`: 4 (4 nodes in total)
* `edges`: \[\[0, 1], \[1, 2], \[0, 3], \[3, 2]] (edges between nodes)
* `succProb`: \[0.3, 0.5, 0.7, 0.1] (probabilities corresponding to each edge)
* `start`: 0 (starting node)
* `end`: 2 (ending node)

We'll walk through the code step by step:

1. The code constructs a graph representation using an adjacency list. The graph would look like this:

```less
0 --> 1 (prob: 0.3), 3 (prob: 0.7)
1 --> 0 (prob: 0.3), 2 (prob: 0.5)
2 --> 1 (prob: 0.5), 3 (prob: 0.1)
3 --> 0 (prob: 0.7), 2 (prob: 0.1)
```

2. The `maxProb` vector is initialized with `[0.0, 0.0, 0.0, 0.0]`, where each element represents the maximum probability of reaching that node.
3. The priority queue (`pq`) is initially empty.
4. The algorithm starts with the starting node `start = 0` and its probability `1.0` and adds it to the priority queue (`pq`).
5. The while loop begins. The priority queue is not empty, so the loop continues.
6. The code extracts the node with the highest probability from the priority queue. In this case, it is `(1.0, 0)`. So `curProb = 1.0` and `curNode = 0`.
7. It checks if the extracted probability `1.0` is less than the maximum probability recorded for node `0`. Since the maximum probability of node `0` is initially `0.0`, the condition is false, and it continues.
8. For each neighbor of node `0`, which are nodes `1` and `3`, it calculates the probability of reaching each neighbor from node `0` by multiplying the current probability `curProb` with the probability of the edge connecting them.
   * For node `1`: `nextProb = 1.0 * 0.3 = 0.3`
   * For node `3`: `nextProb = 1.0 * 0.7 = 0.7`
9. Since both calculated probabilities (`0.3` and `0.7`) are greater than the maximum probability recorded for their respective neighbor nodes (`0.0` for both nodes), it updates `maxProb` with these values: `maxProb[1] = 0.3` and `maxProb[3] = 0.7`. It also adds nodes `1` and `3` to the priority queue with their corresponding probabilities.
10. The while loop continues. The priority queue now contains `(0.7, 3)` and `(0.3, 1)`. The algorithm extracts `(0.7, 3)` from the priority queue.
11. It checks if `0.7` is less than the maximum probability recorded for node `3`. Again, the condition is false, and it continues.
12. For node `2`, the calculated probability is `0.7 * 0.1 = 0.07`. Since this probability is not greater than the current maximum probability of node \`
13. The while loop continues. The priority queue now contains `(0.3, 1)`. The algorithm extracts `(0.3, 1)` from the priority queue.
14. It checks if `0.3` is less than the maximum probability recorded for node `1`. Again, the condition is false, and it continues.
15. For node `2`, the calculated probability is `0.3 * 0.5 = 0.15`. Since this probability is greater than the current maximum probability of node `2` (which is `0.07`), it updates `maxProb[2]` to `0.15`.
16. The while loop continues. The priority queue is now empty, so the loop ends.
17. The maximum probability of reaching the end node (`end = 2`) is `maxProb[2]`, which is `0.15`. Therefore, the algorithm returns `0.15`.

In this example, the maximum probability of reaching node 2 from node 0, considering the edge probabilities, is 0.15. The algorithm explores all possible paths and updates the maximum probabilities as it traverses the graph using a modified Dijkstra's algorithm.

Note that the actual paths taken are not explicitly recorded in this implementation, only the maximum probabilities for each node are tracked.
