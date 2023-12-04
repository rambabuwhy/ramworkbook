# Largest Good Integer: Largest 3-Same-Digit Number in String

`largestGoodInteger` that takes a string `num` as input and returns a string. The function aims to find the largest good integer by identifying three consecutive equal digits in the input string and returning a string containing three occurrences of the maximum digit found.

```cpp
class Solution {
public:
    string largestGoodInteger(string num) {
        
        // Assign 'maxDigit' to the NUL character
        char maxd='\0';
        
        for( int i=0; i<= num.size()-3; i++){
            
            // If 3 consecutive characters are the same,
            if(num[i] == num[i+1] && num[i+1] == num[i+2]){
                maxd = max(maxd, num[i]);
            }
        }
        return maxd == '\0'? "":string(3,maxd);
    }
};

```

Here's a breakdown of the code:

1. `char maxd='\0';`: This initializes a variable `maxd` to the null character.
2. The `for` loop iterates through the characters of the string `num` up to the third-to-last character (`num.size()-3`), checking for three consecutive equal digits.
3. `if(num[i] == num[i+1] && num[i+1] == num[i+2])`: This condition checks if three consecutive characters are the same.
4. `maxd = max(maxd, num[i]);`: If the condition is true, it updates the `maxd` variable with the maximum of its current value and the current character.
5. Finally, the function returns a string containing three occurrences of the maximum digit found, or an empty string if no such digit is found (`maxd == '\0'`).
