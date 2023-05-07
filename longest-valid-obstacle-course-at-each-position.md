# Longest valid obstacle course at each position

Given an array `obstacles` of length `n`, where `obstacles[i]` represents the height of the i-th obstacle, you need to find the length of the longest obstacle course that satisfies the following conditions:

* You can choose any number of obstacles between 0 and i, inclusive.
* You must include the i-th obstacle in the course.
* The chosen obstacles must be in the same order as they appear in the array.
* Every obstacle (except the first) must be taller than or the same height as the obstacle immediately before it.

Return an array `ans` of length `n`, where `ans[i]` represents the length of the longest obstacle course that can be built using obstacles up to position `i` in `obstacles`.

```cpp
class Solution {
public:

    vector<int> longestObstacleCourseAtEachPosition(vector<int>& obstacles) {
        int n = obstacles.size();
        
        vector<int> answer(n, 1); // initialize all values to 1
        vector<int> lis; // stores the longest increasing subsequence so far
        
        for (int i = 0; i < n; ++i) {
            int idx = upper_bound(lis.begin(), lis.end(), obstacles[i]) - lis.begin();
            if (idx == lis.size()) {
                lis.push_back(obstacles[i]);
            } else {
                lis[idx] = obstacles[i];
            }
            answer[i] = idx + 1;
        }
        return answer;
    }
};
```

The idea is to maintain a vector `lis` that records the lowest increasing sequence for each length i, where i is the index of the element in the vector. For example, `lis[2]` stores the lowest number that can be used to form an increasing subsequence of length 3.

Initially, `lis` is empty, and we traverse the `obstacles` vector from left to right. For each element `obstacles[i]`, we find the rightmost position where we can insert it into `lis` to maintain the sorted order. We update the `answer` vector with the length of the increasing sequence that includes the current obstacle `obstacles[i]`.

At the end, we return the `answer` vector that contains the length of the longest obstacle course at each position.

Note that this implementation assumes that the input vector `obstacles` is non-empty.



The time complexity of this algorithm is O(n log n), where n is the length of the input vector `obstacles`. The algorithm iterates over the input vector once, and for each element, it performs a binary search on the `lis` vector, which takes logarithmic time. Therefore, the overall time complexity is proportional to the product of the length of the input vector and the logarithm of the length of the `lis` vector, which is dominated by the latter term. Since the `lis` vector has at most length n, the total time complexity is O(n log n).
