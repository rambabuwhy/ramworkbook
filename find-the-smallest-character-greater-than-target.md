# Find the Smallest Character Greater than Target

Given a sorted array of characters, `letters`, in non-decreasing order, and a character `target`, find the smallest character in `letters` that is lexicographically greater than `target`. If there is no character in `letters` that is greater than `target`, return the first character in `letters`.

**Function Signature:**

```cpp
char nextGreatestLetter(std::vector<char>& letters, char target);
```

**Input:**

* `letters`: A vector of characters (`std::vector<char>`) representing the sorted array of characters.
* `target`: A character (`char`) representing the target character.

**Output:**

* Returns a character (`char`) representing the smallest character in `letters` that is lexicographically greater than `target`, or the first character in `letters` if no such character exists.

To solve the problem, you can use a simple linear search algorithm. Since the array is already sorted in non-decreasing order, you can iterate over the array and find the smallest character that is greater than the target.

```cpp
#include <vector>

char nextGreatestLetter(std::vector<char>& letters, char target) {
    for (char c : letters) {
        if (c > target) {
            return c;
        }
    }
    // If no character is greater than the target, return the first character in letters
    return letters[0];
}

```

To optimize, we use a binary search algorithm to find the smallest character greater than the target. We maintain two pointers, `left` and `right`, which represent the range of indices to search in. We initialize `left` to 0 and `right` to `n - 1`, where `n` is the size of the vector.

In each iteration of the while loop, we calculate the middle index `mid`. If the character at `letters[mid]` is less than or equal to the target, we update `left` to `mid + 1` to search in the right half of the array. Otherwise, we update `result` to `mid` and update `right` to `mid - 1` to search in the left half of the array.

At the end of the loop, `result` will hold the index of the smallest character greater than the target. We return `letters[result % n]` to handle cases where the target is greater than all the characters in the array. The modulo operation ensures that we wrap around to the first character if needed.



```cpp
#include <vector>

char nextGreatestLetter(std::vector<char>& letters, char target) {
    int n = letters.size();
    int left = 0;
    int right = n - 1;
    int result = 0;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (letters[mid] <= target) {
            left = mid + 1;
        } else {
            result = mid;
            right = mid - 1;
        }
    }

    return letters[result % n];
}

int main() {
    std::vector<char> letters = {'a', 'b', 'd', 'f', 'h'};
    char target = 'c';
    char result = nextGreatestLetter(letters, target);
    std::cout << "Smallest character greater than '" << target << "' is '" << result << "'" << std::endl;
    return 0;
}

```

The binary search approach has a time complexity of O(log n), where n is the size of the array, as we are dividing the search space in half at each step. This is more efficient than the linear search approach, especially for large input arrays.
