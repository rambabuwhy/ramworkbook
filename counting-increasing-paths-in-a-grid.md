# Counting Increasing Paths in a Grid

## Problem:

You are given a grid of size MxN, where each cell contains an integer value. Your task is to calculate the total number of paths in the grid such that each path is strictly increasing in value.

A path is a sequence of cells in the grid starting from one cell and moving to adjacent cells in one of the four directions: right, down, left, or up. Two cells are considered adjacent if they share an edge.

In order for a path to be considered increasing, the value of each subsequent cell in the path must be greater than the value of the previous cell.

You need to implement the `Solution` class, which contains the following method:

```cpp
int countPaths(vector<vector<int>>& grid);
```

**Input:**

* The `grid` parameter is a 2D vector of integers representing the grid, where `grid[i][j]` represents the value of the cell at row `i` and column `j`.
* The grid dimensions satisfy 1 <= M, N <= 100.
* The values in the grid satisfy 0 <= grid\[i]\[j] <= 10^9.

**Output:**

* Return an integer representing the total number of increasing paths in the grid.

**Note:**

* The answer may be large, so return the result modulo 10^9 + 7 (1e9 + 7).

**Example:**

```cpp
vector<vector<int>> grid = {{1, 2, 3},
                            {4, 5, 6},
                            {7, 8, 9}};
Solution obj;
int paths = obj.countPaths(grid);
```

**Output:** `paths = 6`

**Explanation:** In the given example, there are six increasing paths in the grid:

* Path 1: (1 -> 2 -> 3 -> 6 -> 9)
* Path 2: (1 -> 2 -> 5 -> 6 -> 9)
* Path 3: (1 -> 4 -> 5 -> 6 -> 9)
* Path 4: (1 -> 4 -> 7 -> 8 -> 9)
* Path 5: (2 -> 3 -> 6 -> 9)
* Path 6: (4 -> 5 -> 6 -> 9)

## Solution:

The program uses dynamic programming and memoization to avoid redundant calculations and optimize the computation of the number of increasing paths in the grid.

```cpp
const int MOD = 1e9 + 7;
const vector<int> dirs = {0, 1, 0, -1, 0};

class Solution {
public:
    int countPaths(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        
        vector<vector<long long>> memo(rows, vector<long long>(cols, -1));
        
        long long totalPaths = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                totalPaths = (totalPaths + dp(grid, i, j, memo)) % MOD;
            }
        }
        
        return static_cast<int>(totalPaths);
    }
    
private:
    long long dp(vector<vector<int>>& grid, int i, int j, vector<vector<long long>>& memo) {
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        
        int rows = grid.size();
        int cols = grid[0].size();
        
        long long result = 1;
        
        for (int d = 0; d < 4; d++) {
            int x = i + dirs[d];
            int y = j + dirs[d + 1];
            
            if (x >= 0 && y >= 0 && x < rows && y < cols && grid[x][y] > grid[i][j]) {
                result = (result + dp(grid, x, y, memo)) % MOD;
            }
        }
        
        memo[i][j] = result;
        return result;
    }
};

```

The main coding pattern used in the program is memoization. Memoization is a technique that allows storing the results of expensive function calls and reusing them when the same inputs occur again. It helps to avoid redundant calculations and optimize the overall performance of the program.

Here's an overview of the coding pattern used in the program:

1. The `countPaths` function is the entry point of the program. It initializes the necessary variables and data structures, such as the `memo` table, to store the cached results.
2. The `countPaths` function iterates through each cell in the grid using nested loops. For each cell, it calls the `dp` function to calculate the number of increasing paths starting from that cell.
3. The `dp` function is a recursive function that calculates the number of increasing paths starting from a given cell `(i, j)` in the grid. It follows the following steps:
   * Check if the result for the current cell is already cached in the `memo` table. If so, return the cached result.
   * Initialize a variable `result` to 1, representing the contribution of the current cell as an increasing sequence.
   * Iterate through the four directions using a loop. For each direction, calculate the next cell's coordinates `(x, y)`.
   * Check if the next cell `(x, y)` is within the grid boundaries and has a greater value than the current cell `(i, j)`.
   * If the condition is met, recursively call `dp` on the next cell and add the result to `result`.
   * Cache the `result` for the current cell in the `memo` table.
   * Return the `result`.
4. The `countPaths` function accumulates the results from each cell's `dp` calculation and returns the final result, which represents the total number of increasing paths in the grid.

Note:

By using memoization, the program avoids redundant calculations by storing and reusing the results of subproblems. This optimization greatly improves the efficiency and performance of the program, especially for larger grids.

In this optimized version, the code maintains the clarity of the original implementation while improving readability. It also includes a few optimizations:

1. Constants (`MOD` and `dirs`) are declared as `const` variables outside the class for better readability and to emphasize that they do not change.
2. The grid's dimensions (`rows` and `cols`) are stored in variables for easier access and readability.
3. The `totalPaths` variable is declared as a `long long` to handle large results.
4. The `countPaths` function is made private, as it is only used internally by the class. This encapsulation improves code organization and readability.
5. The `static_cast<int>(totalPaths)` is used to convert the `long long` result to `int` for the return statement.
