# Shortest Clear Path in a Binary Matrix

You are given an `n x n` binary matrix `grid`, where each cell of the matrix can be either 0 or 1. The matrix represents a grid where 0 denotes a clear cell and 1 denotes a blocked cell. Your task is to find the length of the shortest clear path from the top-left cell (0, 0) to the bottom-right cell (n - 1, n - 1), subject to the following conditions:

1. A clear path is a path consisting of only clear cells (0) that starts at the top-left cell and ends at the bottom-right cell.
2. Two cells are considered adjacent if they share an edge or a corner. In other words, they are connected in one of the eight possible directions: top, top-right, right, bottom-right, bottom, bottom-left, left, or top-left.
3. The length of a clear path is the number of visited cells in that path.

Write a function `int shortestPathBinaryMatrix(vector<vector<int>>& grid)` to solve the problem. The function should return the length of the shortest clear path if it exists; otherwise, it should return -1.

**Function Signature:**

```cpp
int shortestPathBinaryMatrix(vector<vector<int>>& grid)
```

**Input:**

The input parameter `grid` is a 2D vector of integers representing the binary matrix. The matrix has dimensions `n x n` (1 ≤ n ≤ 100). Each element `grid[i][j]` of the matrix is either 0 or 1.

**Output:**

The function should return an integer representing the length of the shortest clear path from the top-left cell to the bottom-right cell. If there is no clear path, return -1.

**Examples:**

1.

Input:

```css
grid = [    [0, 0, 0],
    [1, 1, 0],
    [1, 1, 0]
]
```

Output:

```
5
```

Explanation: The shortest clear path in this case is (0, 0) → (0, 1) → (0, 2) → (1, 2) → (2, 2).

2.

Input:

```css
grid = [    [1, 0, 0],
    [1, 1, 0],
    [1, 1, 0]
]
```

Output:

```diff
-1
```

Explanation: In this case, there is no clear path from the top-left cell to the bottom-right cell because the start cell (0, 0) is blocked.

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
    int n = grid.size();
    if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1) {
        return -1;  // Check if the start or end cell is blocked
    }
    
    vector<vector<int>> directions = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
    
    vector<vector<bool>> visited(n, vector<bool>(n, false));
    visited[0][0] = true;
    
    queue<pair<int, int>> q;
    q.push({0, 0});
    
    int pathLength = 1;
    while (!q.empty()) {
        int size = q.size();
        while (size--) {
            int row = q.front().first;
            int col = q.front().second;
            q.pop();
            
            if (row == n - 1 && col == n - 1) {
                return pathLength;  // Reached the bottom-right cell
            }
            
            for (const auto& dir : directions) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                
                if (newRow >= 0 && newRow < n && newCol >= 0 && newCol < n && !visited[newRow][newCol] && grid[newRow][newCol] == 0) {
                    visited[newRow][newCol] = true;
                    q.push({newRow, newCol});
                }
            }
        }
        
        pathLength++;
    }
    
    return -1;  // No clear path found
}
```

This code uses a breadth-first search (BFS) algorithm to find the shortest clear path in the binary matrix. It starts at the top-left cell and explores its adjacent cells in all eight directions. It marks visited cells to avoid revisiting them and keeps track of the path length. The algorithm continues until it reaches the bottom-right cell or exhausts all possible paths.

Note: This implementation assumes that the input grid is a valid binary matrix, where 0 represents a clear cell and 1 represents a blocked cell.

Let's go through the logic of the code using a simple example.

Suppose we have the following binary matrix grid:

```
1 0 0
1 1 0
1 1 0
```

We want to find the length of the shortest clear path from the top-left cell (0, 0) to the bottom-right cell (2, 2).

1. The code first checks if the start or end cell is blocked (contains a 1). In this example, the start cell (0, 0) is blocked, so it returns -1.
2. Now, let's consider a modified grid where the start cell is clear:

```
0 0 0
1 1 0
1 1 0
```

3. We initialize a `directions` vector with eight possible directions: top-left, top, top-right, left, right, bottom-left, bottom, and bottom-right. These directions define the adjacent cells.
4. We create a `visited` vector to keep track of visited cells. Initially, all cells are marked as unvisited except for the start cell (0, 0), which is set to true.
5. We create a queue to perform a breadth-first search. We enqueue the start cell (0, 0) into the queue.
6. We initialize `pathLength` as 1 to represent the length of the current path.
7.  While the queue is not empty, we process each cell in the queue:

    a. We dequeue a cell (row, col) from the front of the queue.

    b. If we have reached the bottom-right cell (2, 2), we return the current `pathLength` as the shortest clear path length.

    c. Otherwise, we check the eight adjacent cells (neighbors) of the current cell:

    ```css
    i. For each adjacent cell (newRow, newCol), we check if it is within the grid boundaries, not visited, and represents a clear cell (contains a 0).
     
     ii. If these conditions are met, we mark the adjacent cell as visited, enqueue it into the queue, and continue the exploration.
    ```

    d. After processing all the cells in the current level, we increment `pathLength` by 1 to move to the next level.
8. If we exhaust all possible paths and haven't reached the bottom-right cell, it means there is no clear path. In this case, we return -1.

Using the modified grid from step 2, the algorithm would explore the cells in the following order:

```
0 0 0
1 1 0
1 1 0
```

The numbers represent the order in which the cells are visited. The algorithm would return a shortest clear path length of 5.
