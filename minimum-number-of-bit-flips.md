# Minimum number of bit flips

## Problem:

You are given three positive numbers, `a`, `b`, and `c`. Your task is to write a function that calculates the minimum number of bit flips required in `a` and `b` to make the bitwise OR of `a` and `b` equal to `c`.

A flip operation consists of changing any single bit from 1 to 0 or from 0 to 1 in the binary representation of a number.

Write a function `minFlips(a, b, c)` that takes in three integers `a`, `b`, and `c` as input and returns the minimum number of flips required to make `(a | b) == c`, where `|` represents the bitwise OR operation.

**Examples:**

```cpp
minFlips(2, 6, 5) => 3
minFlips(4, 2, 7) => 1
minFlips(1, 2, 3) => 0
```

Note:

* In Example 1, the binary representation of `2` is `10`, `6` is `110`, and `5` is `101`. By flipping the bits in `a` and `b`, we can obtain `1` (`01`) and `4` (`100`) respectively, such that `(1 | 4) == 5`.
* In Example 2, the binary representation of `4` is `100`, `2` is `010`, and `7` is `111`. By flipping the bit in `a`, we can obtain `4` (`100`) and `2` (`010`) such that `(4 | 2) == 7`.
* In Example 3, the binary representation of `1` is `001`, `2` is `010`, and `3` is `011`. As `(1 | 2) == 3`, no bit flips are required.

## Solution:

```cpp
#include <iostream>

int minFlips(int a, int b, int c) {
    int flips = 0;
    
    for (int i = 0; i < 32; i++) {
        bool bitA = (a >> i) & 1;
        bool bitB = (b >> i) & 1;
        bool bitC = (c >> i) & 1;
        
        if ((bitA | bitB) != bitC) {
            if (bitC == 1) {
                flips++;
            } else {
                flips += (bitA == 1) + (bitB == 1);
            }
        }
    }
    
    return flips;
}

int main() {
    // Example usage
    int a = 2, b = 6, c = 5;
    int flips = minFlips(a, b, c);
    std::cout << "Minimum flips: " << flips << std::endl;
    
    return 0;
}

```

Explanation:

1. The function `minFlips` takes three integers `a`, `b`, and `c` as input and returns the minimum number of flips required to make `a | b` equal to `c`.
2. We iterate through the bits of `a`, `b`, and `c` using a loop that runs 32 times (assuming integers are 32-bit).
3. Inside the loop, we extract the `i`th bit from `a`, `b`, and `c` using bitwise operations and store them in `bitA`, `bitB`, and `bitC` variables, respectively.
4. We check if `(bitA | bitB) != bitC` to determine if a flip is required for the current bit.
5. If `bitC` is 1 and `(bitA | bitB)` is not equal to 1, it means that at least one of the bits in `a` or `b` must be flipped to make `a | b` equal to `c`. In this case, we increment the `flips` count by 1.
6. If `bitC` is 0, we check if either `bitA` or `bitB` is 1. If either of them is 1, it means that a flip is required to make `a | b` equal to `c`. In this case, we increment the `flips` count accordingly.
7. Finally, we return the total `flips` count, which represents the minimum number of flips required.
