# Counting Equal Row-Column Pairs in a Matrix

## Problem:

Given a square matrix `grid` of size `n x n`, where `n` is the number of rows and columns, you need to count the number of pairs `(ri, cj)` such that the elements in row `ri` and column `cj` are equal, considering the order of elements.

A pair `(ri, cj)` is considered equal if the elements in row `ri` and column `cj` are the same and appear in the same order. In other words, the elements of `grid[ri]` and the elements of the column obtained by considering the elements `grid[0][cj], grid[1][cj], ..., grid[n-1][cj]` are equal when compared element by element.

Your task is to implement a function that takes in the matrix `grid` as input and returns the count of such equal row-column pairs.

**Function Signature:**

```cpp
int countEqualRowColumnPairs(std::vector<std::vector<int>>& grid)
```

**Input:**

* The input matrix `grid` is a square matrix with dimensions `n x n` (1 <= n <= 100).
* The elements in the matrix `grid` are integers.

**Output:**

* The function should return an integer representing the count of equal row-column pairs.

**Example:**

```cpp
std::vector<std::vector<int>> grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
int result = countEqualRowColumnPairs(grid);
// The matrix contains the following equal row-column pairs:
// (0, 0): [1, 4, 7] and [1, 4, 7]
// (1, 1): [2, 5, 8] and [2, 5, 8]
// (2, 2): [3, 6, 9] and [3, 6, 9]
// So, the count of equal row-column pairs is 3.
// Therefore, the 'result' will be 3.
```

**Note:**

* The input matrix `grid` may contain duplicate elements.
* The elements in each row and column will be within the range of integer values.
* The elements should be compared considering both their values and the order in which they appear.

## Solution:

```cpp
#include <vector>
#include <unordered_map>
#include <string>
#include <algorithm>

int equalPairs(std::vector<std::vector<int>>& grid) {
    int count = 0;
    int n = grid.size();
    
    // Keep track of the frequency of each row.
    std::unordered_map<std::string, int> rowCounter;
    for (const auto& row : grid) {
        std::string rowString = "";
        for (int element : row) {
            rowString += std::to_string(element) + ",";
        }
        rowCounter[rowString]++;
    }

    // Add up the frequency of each column in the map.
    for (int c = 0; c < n; c++) {
        std::string colString = "";
        for (int r = 0; r < n; r++) {
            colString += std::to_string(grid[r][c]) + ",";
        }
        count += rowCounter[colString];
    }

    return count;
}

```

This C++ code converts each row and column into a string representation using `std::to_string()` and concatenates the elements separated by commas. It then uses an `std::unordered_map<std::string, int>` to count the frequency of each row and retrieve the frequency of each column. Finally, it adds up the frequencies of the columns to get the total count of equal row-column pairs.

Let's break down the logic of the provided code snippet step by step:

1. Initialize the `count` variable to 0, which will be used to keep track of the number of equal row-column pairs.
2. Get the size of the input matrix `grid` using `grid.length`, assuming `grid` is a square matrix.
3. Create an `HashMap` named `rowCounter` to keep track of the frequency of each row. This map will store the string representation of a row as the key and the frequency as the value.
4. Iterate over each row in the `grid` matrix using a for-each loop. Inside the loop:
   * Convert the current row into a string representation using `Arrays.toString(row)`. This converts the array to a string with the elements enclosed in brackets and separated by commas.
   * Increment the frequency of the current row in the `rowCounter` map using `rowCounter.put(rowString, 1 + rowCounter.getOrDefault(rowString, 0))`. It retrieves the current frequency of the row (0 if it doesn't exist) and increments it by 1, then puts it back into the map.
5. Iterate over each column in the `grid` matrix using a for loop. Inside the loop:
   * Create an `int` array named `colArray` to store the elements of the current column.
   * Iterate over each row in the `grid` matrix again using a for loop. Inside this nested loop, assign the element at column index `c` to the corresponding index in `colArray` (i.e., `colArray[r] = grid[r][c]`).
   * Convert the `colArray` into a string representation using `Arrays.toString(colArray)`.
   * Add the frequency of the current column stored in the `rowCounter` map to the `count` variable using `count += rowCounter.getOrDefault(Arrays.toString(colArray), 0)`. It retrieves the frequency of the current column (0 if it doesn't exist) and adds it to the count.
6. Finally, return the `count` variable, which represents the total number of equal row-column pairs.

In summary, the code iterates over each row of the matrix, converts them into string representations, and stores the frequency of each row in a map. Then, it iterates over each column, converts them into string representations, and retrieves their frequencies from the map, adding them to the count. This approach counts the number of equal row-column pairs by comparing their string representations.
