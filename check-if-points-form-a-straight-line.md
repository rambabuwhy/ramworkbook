# Check if Points Form a Straight Line

## Problem:

You are given an array of 2D coordinates, `coordinates`, where `coordinates[i] = [x, y]` represents the coordinates of a point in the XY plane. Your task is to determine whether these points lie on a straight line.

Write a function `bool checkStraightLine(vector<vector<int>>& coordinates)` that takes in the `coordinates` array and returns `true` if all the points lie on the same straight line, or `false` otherwise.

**Example:**

```cpp
vector<vector<int>> coordinates = {{1, 1}, {2, 2}, {3, 3}, {4, 4}, {5, 5}};
bool result = checkStraightLine(coordinates);
```

**Output:**

The function should return `true`, as all the points `(1, 1), (2, 2), (3, 3), (4, 4), (5, 5)` lie on the same straight line.

## Solution:

The logic behind this approach is that if the cross product of the slopes between each point and the first point is zero, it indicates that all the slopes are equal, and the points lie on the same line. The cross product equality test is a more robust method to handle cases where the slopes involve integer division or potential precision errors with floating-point calculations.

```cpp
#include <iostream>
#include <vector>

bool checkStraightLine(std::vector<std::vector<int>>& coordinates) {
    int n = coordinates.size();
    
    if (n <= 2)
        return true;
    
    int x0 = coordinates[0][0];
    int y0 = coordinates[0][1];
    int x1 = coordinates[1][0];
    int y1 = coordinates[1][1];
    
    // Calculate the slope between the first two points
    int dx = x1 - x0;
    int dy = y1 - y0;
    
    // Check if all other points lie on the same line
    for (int i = 2; i < n; i++) {
        int xi = coordinates[i][0];
        int yi = coordinates[i][1];
        
        // Calculate the slope between the current point and the first point
        int currDx = xi - x0;
        int currDy = yi - y0;
        
        // If the cross product of the slopes is non-zero, points are not on the same line
        if (dx * currDy != dy * currDx)
            return false;
    }
    
    return true;
}

int main() {
    // Example usage
    std::vector<std::vector<int>> coordinates = {{0, 0}, {0, 1}, {0, -1}};
    
    if (checkStraightLine(coordinates))
        std::cout << "Points form a straight line." << std::endl;
    else
        std::cout << "Points do not form a straight line." << std::endl;
    
    return 0;
}

```

Here's a step-by-step explanation of the logic used in the code:

1. The `checkStraightLine` function takes a 2D vector `coordinates` as input, where each inner vector represents the `[x, y]` coordinate of a point.
2. It first checks if the number of points in the `coordinates` vector is less than or equal to 2. If so, it returns `true` because any two points can be considered as forming a straight line.
3. Next, it extracts the coordinates of the first two points, `(x0, y0)` and `(x1, y1)`.
4.  The code calculates the differences in x and y coordinates between the first two points:

    * `dx = x1 - x0`
    * `dy = y1 - y0`

    These differences represent the slope between the first two points.
5. The code then iterates through the remaining points in the `coordinates` vector, starting from the third point.
6. For each point `(xi, yi)`, it calculates the differences in x and y coordinates between the current point and the first point:
   * `currDx = xi - x0`
   * `currDy = yi - y0`
7.  The code checks if the cross product of the slopes is non-zero:

    * `dx * currDy != dy * currDx`

    The cross product is used instead of the direct comparison of slopes `(dy / dx) != (currDy / currDx)` to avoid potential floating-point precision issues.
8. If the cross product is non-zero for any point, it means that the points are not on the same line, and the function returns `false`.
9. If the code finishes iterating through all the points without finding a non-zero cross product, it means that all the points lie on the same line, and the function returns `true`.
