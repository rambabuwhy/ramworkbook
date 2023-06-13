# Matrix Diagonal Sum

## Problem:

Given a square matrix `mat`, return the sum of the matrix diagonals.

The matrix diagonals are defined as follows:

* The primary diagonal is the diagonal that starts at element `mat[0][0]` and ends at element `mat[n-1][n-1]`, where `n` is the size of the square matrix.
* The secondary diagonal is the diagonal that starts at element `mat[0][n-1]` and ends at element `mat[n-1][0]`.

The function `diagonalSum` should return the sum of all the elements on the primary diagonal and all the elements on the secondary diagonal that are not part of the primary diagonal.

If the size of the matrix is odd, exclude the center element from the sum.

{% hint style="info" %}


Input: mat = \[\[1,2,3], \[4,5,6], \[7,8,9]]

Output: 25

Explanation: The matrix diagonals are:

* Primary diagonal: \[1, 5, 9]
* Secondary diagonal: \[3, 5, 7] The sum of all elements on the primary and secondary diagonals that are not part of the primary diagonal is 1 + 3 + 7 + 9 = 20, and the sum of all elements on the primary diagonal is 1 + 5 + 9 = 15. The total sum is 20 + 15 = 25.
{% endhint %}

## Solution:

Here's an example implementation in C++:

```cpp
#include <vector>

int diagonalSum(std::vector<std::vector<int>>& mat) {
    int sum = 0;
    int n = mat.size();
    for (int i = 0; i < n; i++) {
        sum += mat[i][i]; // primary diagonal
        sum += mat[i][n - i - 1]; // secondary diagonal
    }
    if (n % 2 == 1) { // exclude the center element if n is odd
        sum -= mat[n / 2][n / 2];
    }
    return sum;
}

```

This function takes a two-dimensional vector `mat` representing the square matrix and returns the sum of its diagonal elements. The function iterates over each row and column index and adds the element at that index to the sum if it is on the primary diagonal (`i == j`) or the secondary diagonal (`i + j == n - 1`), but not both (the center element is counted twice if `n` is odd). Finally, the function returns the total sum.

The code I provided has a time complexity of O(n^2), where n is the size of the matrix. This is because the code iterates over each row and column index in the matrix and performs a constant number of operations for each index. Therefore, the time complexity is proportional to the size of the matrix.

This is an optimal time complexity for this problem, as we need to visit each element of the matrix at least once in order to compute the sum of its diagonals. Since the matrix has n^2 elements, the time complexity cannot be better than O(n^2).

However, there are some minor optimizations we can make to the code. For example, instead of accessing `mat[i][n - i - 1]` for each index `(i, j)`, we can compute `n - i - 1` once and store it in a variable. This reduces the number of subtractions performed and may lead to a slight performance improvement. Additionally, we can avoid the conditional statement in the loop by initializing `sum` to the value of `mat[n/2][n/2]` if `n` is odd and adjusting the loop condition accordingly.
