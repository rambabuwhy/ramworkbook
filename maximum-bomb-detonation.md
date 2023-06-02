# Maximum Bomb Detonation

You are given a list of bombs represented as a 0-indexed 2D integer array `bombs`. Each bomb is represented by three values: `[xi, yi, ri]`, where `xi` and `yi` denote the X and Y coordinates of the bomb's location, and `ri` denotes the radius of its range.

A bomb's range is defined as the area where its effect can be felt, which is in the shape of a circle centered at the bomb's location.

You can choose to detonate a single bomb. When a bomb is detonated, it will trigger the detonation of all bombs within its range. Those bombs, in turn, will detonate any bombs within their ranges, and so on.

Write a function `maximumDetonation` that takes the list of bombs `bombs` as input and returns the maximum number of bombs that can be detonated if you are allowed to detonate only one bomb.

**Example:**

```cpp
Input: bombs = [[2,1,3],[6,1,4]]
Output: 2
```

Here's a more detailed explanation of the code logic:

1. The `dfs` function performs a depth-first search (DFS) to count the number of bombs that can be detonated starting from a given bomb. It uses recursion and a boolean array to keep track of the detonation status of each bomb.
2. The `maximumDetonation` function calculates the maximum number of bombs that can be detonated. It creates an adjacency list to represent the connections between bombs and then performs DFS for each bomb, finding the maximum count of detonated bombs.
3. The code iterates through each bomb and checks the range of each bomb by calculating the squared distance between bombs. It builds the adjacency list by adding adjacent bombs that can be detonated.
4. Finally, the code performs DFS for each bomb, keeping track of the maximum number of detonated bombs found.
5. The function returns the maximum number of bombs that can be detonated.

By using DFS and an adjacency list, the code effectively explores the connections between bombs to determine the maximum number of bombs that can be detonated.

```cpp
// Perform depth-first search (DFS) to count the number of detonated bombs
int dfs(int i, const vector<vector<int>>& adjacencyList, vector<bool>& detonated) {
    // Mark the current bomb as detonated
    detonated[i] = true;

    // Initialize the count of detonated bombs to 1 (counting the current bomb)
    int count = 1;

    // Explore the adjacency list for the current bomb
    for (int j : adjacencyList[i]) {
        // If the adjacent bomb hasn't been detonated yet, perform DFS on it
        if (!detonated[j]) {
            count += dfs(j, adjacencyList, detonated);
        }
    }

    return count;
}

// Calculate the maximum number of bombs that can be detonated
int maximumDetonation(const vector<vector<int>>& bombs) {
    int maxDetonations = 0;
    int numBombs = bombs.size();

    // Create an adjacency list to represent the connections between bombs
    vector<vector<int>> adjacencyList(numBombs);

    // Build the adjacency list by checking the range of each bomb
    for (int i = 0; i < numBombs; ++i) {
        long long xi = bombs[i][0], yi = bombs[i][1], ri = bombs[i][2];
        long long riSquared = ri * ri;

        for (int j = 0; j < numBombs; ++j) {
            if (i == j) continue; // Skip the same bomb

            long long xj = bombs[j][0], yj = bombs[j][1];

            // Calculate the squared distance between the two bombs
            long long distanceSquared = (xi - xj) * (xi - xj) + (yi - yj) * (yi - yj);

            // Check if the current bomb can detonate the adjacent bomb
            if (distanceSquared <= riSquared) {
                adjacencyList[i].push_back(j);
            }
        }
    }

    // Perform DFS for each bomb to find the maximum number of detonations
    for (int i = 0; i < numBombs; ++i) {
        vector<bool> detonated(numBombs, false); // Initialize the detonation status for each bomb
        int detonations = dfs(i, adjacencyList, detonated);
        maxDetonations = max(maxDetonations, detonations);
    }

    return maxDetonations;
}

```

The time complexity of the provided solution is O(N^3), where N is the number of bombs.

1. Building the adjacency list: This step takes O(N^2) time because, for each bomb, we iterate through all other bombs to check if they lie within the range. This results in a total of N^2 comparisons.
2. Depth-First Search (DFS): The DFS function is called for each bomb. In the worst case, where all bombs are connected to each other, the DFS can visit all the bombs. Since the maximum depth of the recursion is N, the time complexity for DFS is O(N).
3. Performing DFS for each bomb: This step takes O(N^2) time because we perform DFS for each of the N bombs.

Therefore, the overall time complexity is O(N^3) due to the N^2 time complexity for building the adjacency list and the N^2 time complexity for performing DFS for each bomb.

It's worth noting that the solution can be optimized by using more efficient data structures and algorithms to build the adjacency list and perform DFS. With optimized implementations, it's possible to achieve a better time complexity, such as O(N^2) or even O(N\*log(N)).

