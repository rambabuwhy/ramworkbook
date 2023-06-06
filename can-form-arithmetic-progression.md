# Can form arithmetic Progression

Given an array of numbers `arr`, determine if it is possible to rearrange the elements of the array to form an arithmetic progression. An arithmetic progression is a sequence of numbers in which the difference between any two consecutive elements is the same. Return `true` if such a rearrangement is possible; otherwise, return `false`.

Function Signature:

```cpp
bool canFormArithmeticProgression(std::vector<int>& arr);
```

Input:

* The input parameter `arr` is a reference to a vector of integers representing the array.

Output:

* The function should return a boolean value indicating whether it is possible to rearrange the elements of the array to form an arithmetic progression.

Here's an example implementation in C++ that checks if an array can be rearranged to form an arithmetic progression:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

bool canFormArithmeticProgression(std::vector<int>& arr) {
    int n = arr.size();
    if (n < 2) {
        // An array with less than 2 elements is always considered an arithmetic progression
        return true;
    }

    // Sort the array in ascending order
    std::sort(arr.begin(), arr.end());

    // Calculate the common difference between consecutive elements
    int diff = arr[1] - arr[0];

    // Check if the difference between any two consecutive elements is the same
    for (int i = 2; i < n; i++) {
        if (arr[i] - arr[i - 1] != diff) {
            return false;
        }
    }

    // If all differences are the same, it's an arithmetic progression
    return true;
}

int main() {
    // Example usage
    std::vector<int> arr = {4, 2, 6, 8};  // can be rearranged to form an arithmetic progression: {2, 4, 6, 8}
    bool result = canFormArithmeticProgression(arr);
    if (result) {
        std::cout << "The array can be rearranged to form an arithmetic progression.\n";
    } else {
        std::cout << "The array cannot be rearranged to form an arithmetic progression.\n";
    }
    
    return 0;
}

```

The provided implementation is relatively straightforward and has a time complexity of O(n log n) due to the sorting operation using `std::sort`. Sorting the array is necessary to identify the common difference between consecutive elements accurately.

While the implementation is correct, we can optimize it further to achieve a linear time complexity of O(n). Here's an optimized version:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

bool canFormArithmeticProgression(std::vector<int>& arr) {
    int n = arr.size();
    if (n < 2) {
        // An array with less than 2 elements is always considered an arithmetic progression
        return true;
    }

    // Find the minimum and maximum elements in the array
    int minElement = arr[0];
    int maxElement = arr[0];
    for (int i = 1; i < n; i++) {
        minElement = std::min(minElement, arr[i]);
        maxElement = std::max(maxElement, arr[i]);
    }

    // Calculate the common difference between consecutive elements
    int diff = (maxElement - minElement) / (n - 1);

    // Check if the difference between any two consecutive elements is the same
    std::unordered_set<int> numSet(arr.begin(), arr.end());
    for (int i = 0; i < n; i++) {
        int expectedNextElement = arr[i] + diff;
        if (numSet.find(expectedNextElement) == numSet.end()) {
            return false;
        }
    }

    // If all differences are the same, it's an arithmetic progression
    return true;
}

int main() {
    // Example usage
    std::vector<int> arr = {4, 2, 6, 8};  // can be rearranged to form an arithmetic progression: {2, 4, 6, 8}
    bool result = canFormArithmeticProgression(arr);
    if (result) {
        std::cout << "The array can be rearranged to form an arithmetic progression.\n";
    } else {
        std::cout << "The array cannot be rearranged to form an arithmetic progression.\n";
    }

    return 0;
}

```

In the optimized version, we find the minimum and maximum elements in the array using a single pass. This allows us to calculate the common difference accurately. Then, we store all the elements of the array in an unordered set for efficient lookup.

Next, we iterate over each element of the array and check if the expected next element (`arr[i] + diff`) exists in the set. If it doesn't, we return false immediately. Otherwise, we continue checking the remaining elements.

The optimized version eliminates the need for sorting, resulting in a linear time complexity of O(n).

Note:

Let me explain the logic behind the line `int diff = (maxElement - minElement) / (n - 1)` in the optimized code.

In an arithmetic progression, the difference between any two consecutive elements is constant. To determine this common difference, we can calculate the difference between the maximum and minimum elements in the array and divide it by the number of gaps between the elements.

Consider an example: `{2, 4, 6, 8}`. The minimum element is 2, and the maximum element is 8. In this case, there are three gaps between the elements: (2, 4), (4, 6), and (6, 8). The difference between the maximum and minimum elements is 8 - 2 = 6.

To obtain the common difference, we divide the difference by the number of gaps, which is `(n - 1)` in this case, where `n` is the number of elements in the array. So, in this example, the common difference would be `6 / (4 - 1) = 2`.

By using this formula, we can calculate the common difference between consecutive elements and later check if the expected next element (`arr[i] + diff`) exists in the array.
