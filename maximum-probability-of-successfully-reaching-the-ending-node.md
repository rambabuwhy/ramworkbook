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
