# Missing number finder

Given two 0-indexed integer arrays `nums1` and `nums2`, find all the distinct integers that are present in `nums1` but not in `nums2`, and all the distinct integers that are present in `nums2` but not in `nums1`.

Return a vector `answer` of size 2, where `answer[0]` is a vector of all the distinct integers in `nums1` that are not present in `nums2`, and `answer[1]` is a vector of all the distinct integers in `nums2` that are not present in `nums1`.

```cpp
#include <vector>
#include <unordered_set>

std::vector<std::vector<int>> findMissingNumbers(std::vector<int>& nums1, std::vector<int>& nums2) {
    // Create two unordered sets to store the unique integers in nums1 and nums2
    std::unordered_set<int> set1(nums1.begin(), nums1.end());
    std::unordered_set<int> set2(nums2.begin(), nums2.end());

    // Create two more unordered sets to store the integers that are only in nums1 and nums2
    std::unordered_set<int> onlyIn1;
    std::unordered_set<int> onlyIn2;

    // Iterate through set1 and check if each integer is also in set2
    // If not, add it to onlyIn1
    for (auto num : set1) {
        if (set2.find(num) == set2.end()) {
            onlyIn1.insert(num);
        }
    }

    // Iterate through set2 and check if each integer is also in set1
    // If not, add it to onlyIn2
    for (auto num : set2) {
        if (set1.find(num) == set1.end()) {
            onlyIn2.insert(num);
        }
    }

    // Create a vector of vectors to store the answer
    std::vector<std::vector<int>> answer(2);

    // Convert the unordered sets onlyIn1 and onlyIn2 to vectors and store them in answer
    answer[0].insert(answer[0].end(), onlyIn1.begin(), onlyIn1.end());
    answer[1].insert(answer[1].end(), onlyIn2.begin(), onlyIn2.end());

    // Return the answer
    return answer;
}

```

The function takes two input vectors `nums1` and `nums2`, and returns a vector of two vectors as the output. It first creates two unordered sets `set1` and `set2` to store the unique integers in `nums1` and `nums2`, respectively. Then, it creates two more unordered sets `onlyIn1` and `onlyIn2` to store the integers that are only in `nums1` and `nums2`, respectively.

Next, it iterates through `set1` and checks if each integer is also in `set2`. If not, it adds the integer to `onlyIn1`. Similarly, it iterates through `set2` and checks if each integer is also in `set1`. If not, it adds the integer to `onlyIn2`.

Finally, it creates a vector of vectors `answer` to store the output. It converts the unordered sets `onlyIn1` and `onlyIn2` to vectors and stores them in `answer[0]` and `answer[1]`, respectively. It then returns `answer`.

Time Complexity:

* The creation of the unordered sets `set1` and `set2` takes O(n1 + n2) time, where n1 and n2 are the sizes of `nums1` and `nums2`, respectively.
* The iteration through `set1` and `set2` to find the elements only present in one set takes O(n1 + n2) time.
* The conversion of `onlyIn1` and `onlyIn2` unordered sets to vectors takes O(m1 + m2) time, where m1 and m2 are the sizes of the resulting vectors, respectively.
* Therefore, the total time complexity of the program is O(n1 + n2 + m1 + m2).

Space Complexity:

* The space required for the unordered sets `set1`, `set2`, `onlyIn1`, and `onlyIn2` is proportional to the number of distinct elements in `nums1` and `nums2`.
* Therefore, the space complexity of the program is O(n1 + n2).

Overall, the program has a time complexity of O(n1 + n2 + m1 + m2) and a space complexity of O(n1 + n2), where n1 and n2 are the sizes of `nums1` and `nums2`, respectively, and m1 and m2 are the sizes of the resulting vectors containing the missing numbers.
