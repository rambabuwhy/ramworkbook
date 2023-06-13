# Smallest Sorted Ranges

## Problem:&#x20;

Given a sorted array of unique integers, `nums`, the task is to find the smallest possible list of ranges that covers all the numbers in the array exactly. Each element in `nums` should be covered by exactly one range, and no other integers should be included in the ranges.

Write a function `findSmallestRanges` in C++ that takes an input array `nums` and returns a vector of strings representing the smallest sorted list of ranges.

The function should adhere to the following specifications:

* The input array `nums` is sorted in non-decreasing order.
* Each range should be represented as a string in the output vector.
* If a range consists of a single element, it should be represented as "a" where 'a' is the value of the element.
* If a range consists of multiple elements, it should be represented as "a->b" where 'a' is the starting element and 'b' is the ending element of the range.
* The output vector should be sorted in non-decreasing order of the ranges.

**Example:**

```cpp
cppCopy codevector<int> nums = {0, 1, 2, 4, 5, 7};

vector<string> ranges = findSmallestRanges(nums);

// Expected output: {"0->2", "4->5", "7"}
```

In the given example, the input array `nums` contains the elements {0, 1, 2, 4, 5, 7}. The smallest list of ranges that cover all these numbers exactly is {"0->2", "4->5", "7"}.

## Solution:

To solve this problem in C++, you can iterate through the sorted array `nums` and merge consecutive elements to form ranges. Here's an implementation that achieves this:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<string> summaryRanges(vector<int>& nums) {
    vector<string> result;
    int n = nums.size();
    int i = 0;

    while (i < n) {
        int start = nums[i];
        int end = start;

        // Find the end of the consecutive range
        while (i + 1 < n && nums[i + 1] == nums[i] + 1) {
            end = nums[i + 1];
            i++;
        }

        // Check if the range has only one element or multiple elements
        if (start == end) {
            result.push_back(to_string(start));  // Single element range
        } else {
            result.push_back(to_string(start) + "->" + to_string(end));  // Multiple element range
        }

        i++;
    }

    return result;
}

int main() {
    vector<int> nums = {0, 1, 2, 4, 5, 7};

    // Get the summary ranges
    vector<string> ranges = summaryRanges(nums);

    // Print the ranges
    for (const string& range : ranges) {
        cout << range << " ";
    }

    return 0;
}

```

In this code, the `summaryRanges` function takes a sorted array `nums` as input and returns a vector of strings containing the smallest sorted list of ranges that cover all the numbers in `nums`. The `main` function demonstrates an example usage by creating an array `nums` and printing the resulting ranges.

The `summaryRanges` function uses two pointers `i` and `start` to iterate through the array. It checks if the current element and the next element form a consecutive range. If they do, it updates the `end` pointer accordingly and increments `i`. If not, it adds the range to the result vector.

Finally, the `main` function calls `summaryRanges` with the input array and prints the resulting ranges. In this example, the output will be:

```rust
rustCopy code0->2 4->5 7
```

which represents the ranges \[0, 2], \[4, 5], and \[7].

It has a time complexity of O(n), where n is the number of elements in the input array `nums`. This is because the code only iterates through the array once, merging consecutive elements to form ranges.
