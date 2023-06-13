# Number of Subsequences that satisfy the given sum

## Problem:

You are given an array of integers `nums` and an integer `target`. Compute the number of non-empty subsequences of `nums` such that the sum of the minimum and maximum element in the subsequence is less than or equal to `target`. Return the result modulo 10^9 + 7.

**Example**

Input: `nums = [3, 1, 2, 4], target = 6`

Output: `7`

Explanation: The valid subsequences are \[1], \[2], \[3], \[1, 2], \[1, 3], \[1, 2, 3], and \[2, 3].

## Solution:

{% code lineNumbers="true" %}
```cpp

int numSubseq(vector<int>& nums, int target) {
        
    //sort the input array
    sort(nums.begin(), nums.end());
    int n = nums.size();

    //precompute the powers of 2
    int pow2[nums.size()+1];
    const int MOD = 1e9 + 7;
    pow2[0] = 1;
    for (int i = 1; i <= nums.size(); i++) {
        pow2[i] = (pow2[i-1] * 2) % MOD;
    }
        
    int left = 0, right = n - 1;
    int ans = 0;
    while (left <= right) {
        if (nums[left] + nums[right] > target) {
            right--;
        } else {
            int len = right - left;
            ans = (ans + pow2[len]) % MOD;
            left++;
        }
    }
    return ans;   
}
```
{% endcode %}

We can solve this problem in O(n) time using a two-pointer approach. First, we sort the array in non-decreasing order. Then, we use two pointers "left" and "right" to find all the valid subsequences. At each step, if the sum of the minimum and maximum element on the current subsequence is greater than "target", we decrement "right". Otherwise, we add 2^len to the answer, where "len" is the length of the current subsequence, and increment "left". To compute the powers of 2 modulo "MOD", we precompute the values of 2^i mod "MOD" for all i from 0 to n, where n is the maximum size of the input array. We store these values in an array "pow2", which is initialized once at the beginning of the program using the function "init\_pow2".

Time Complexity: O(n log n), where n is the size of the input array.
