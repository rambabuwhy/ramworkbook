# Determine the sign

## Problem:

Determine the sign of the product of all elements in an integer array. To determine the sign of the product of all elements in an integer array. Specifically, given an array of integers `nums`, the function `arraySign` returns:

* 1 if the product of all elements in `nums` is positive.
* \-1 if the product of all elements in `nums` is negative.
* 0 if the product of all elements in `nums` is equal to 0.

In other words, the function `arraySign` determines whether the product of all elements in the array is positive, negative, or zero, without actually computing the product itself. Instead, it only considers the sign of each individual element in the array.

## Solution:

```cpp
int arraySign(vector<int>& nums) {
    // Initialize sign to positive 1
    int sign = 1;
    // Loop through each element in nums
    for(auto num:nums){
        // If num is negative, flip the sign by multiplying sign by -1
        if(num < 0) {
            sign = sign * -1;
        }
        // If num is 0, the product will be 0, so return 0
        else if(num == 0) {
            return 0;
        }
    }
    // Return the final sign of the product
    return sign;
}

```

The `arraySign` function works as follows:

1. Initialize `sign` to 1.
2. Loop through each element in `nums`.
3. For the first element, `-2`, the condition `num < 0` is true, so we multiply `sign` by `-1`, which gives us `sign = -1`.
4. For the second element, `3`, the condition `num < 0` is false, so we do nothing.
5. For the third element, `0`, the condition `num == 0` is true, so we return 0 immediately.
6. For the fourth element, `-4`, the condition `num < 0` is true, so we multiply `sign` by `-1` again, which gives us `sign = 1`.
7. For the fifth and final element, `1`, the condition `num < 0` is false, so we do nothing.
8. We have now processed all elements in the array. The final value of `sign` is 1, which means that the product of all elements in `nums` is positive.

Therefore, the `arraySign` function would return `1` for the input array `nums = [-2, 3, 0, -4, 1]`.

The time complexity of the `arraySign` function is O(n), where n is the number of elements in the input array `nums`.

This is because the function simply loops through each element in the array once, and performs a constant amount of work for each element. The work done for each element includes a single comparison, a single multiplication, and a single return statement (in the case where the element is 0).

Since the function performs a constant amount of work for each element, the time complexity is linear in the number of elements in the array, which gives us O(n). This means that the function is able to determine the sign of the product of all elements in the array in a time that scales linearly with the size of the array.

Overall, this makes the `arraySign` function a very efficient and scalable solution for determining the sign of the product of an integer array.
