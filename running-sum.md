# Running Sum

## Problem:

Given an array `nums`, calculate the running sum of `nums`, where `runningSum[i]` is the sum of the first `i+1` elements of `nums`.

The output shows that the running sum of the input array `{1, 2, 3, 4, 5}` is `{1, 3, 6, 10, 15}`, which is the sum of the first i+1 elements of the input array.

## Solution:

An optimized code that can calculate the running sum of an array in linear time complexity, O(n), where n is the size of the array. This code avoids creating an extra vector and does the calculation in-place, using only the input array. Here's the C++ code for the optimized solution

{% code lineNumbers="true" %}
```cpp
vector<int> runningSum(vector<int>& nums) {
    // Loop through the array and calculate the running sum
    for(int i = 1; i < nums.size(); i++) {
        nums[i] += nums[i-1];
    }
    
    // Return the modified input array, which now represents the running sum
    return nums;
}
```
{% endcode %}

In this optimized code, we use a single loop to calculate the running sum in-place. We start from the second element of the input array (i.e., `i = 1`), and for each element at index `i`, we add the value of the previous element (i.e., `nums[i-1]`) to the current element (i.e., `nums[i]`), which represents the running sum up to the current element. We modify the input array directly, without the need for an extra vector.

Finally, we return the modified input array, which now represents the running sum.

you can also use the `std::partial_sum` function from the C++ Standard Library to calculate the running sum of an array. The `partial_sum` function takes two iterators as arguments and calculates the partial sum of the elements between the iterators. Here's the C++ code for using `partial_sum` to calculate the running sum of an array:

{% code lineNumbers="true" %}
```cpp
vector<int> runningSum(vector<int>& nums) { 
    partial_sum(nums.begin(), nums.end(), nums.begin());
    return nums;
}
```
{% endcode %}

In this code, we pass the `begin` and `end` iterators of the `nums` vector to the `partial_sum` function, along with the `begin` iterator again as the output iterator. This calculates the partial sum of the elements between the `begin` and `end` iterators and stores the result in the `nums` vector.

Finally, we print the modified `nums` vector to the console, which should be `{1,3,6,10}` (the running sum of the input array).

Note that this solution modifies the input vector in-place and does not require an additional output vector, making it memory-efficient.
