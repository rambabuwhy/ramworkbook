# Maximum number of vowel

Given a string `s` and an integer `k`, find the maximum number of vowel letters in any substring of `s` with length `k`.

A vowel letter in English is any one of 'a', 'e', 'i', 'o', or 'u'.

Write a function `maxVowels` that takes in two parameters:

* a string `s` (1 <= s.length() <= 10^5), where each character is a lowercase English letter, and
* an integer `k` (1 <= k <= s.length())

The function should return an integer representing the maximum number of vowel letters in any substring of `s` with length `k`.

If there are multiple substrings with the same maximum number of vowels, return any one of them.

{% code lineNumbers="true" %}
```cpp
int maxVowels(string s, int k) {
    int maxVowelCount = 0;  // initialize the maximum vowel count to be 0
    int vowelCount = 0;     // initialize the vowel count to be 0
    for (int i = 0; i < k; i++) {
        // count the number of vowels in the first k characters
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i' || s[i] == 'o' || s[i] == 'u') {
            vowelCount++;
        }
    }
    maxVowelCount = vowelCount;  // update the maximum vowel count with the count of the first k characters
    for (int i = k; i < s.length(); i++) {
        // slide the window of size k one character to the right and count the number of vowels in the new substring
        if (s[i - k] == 'a' || s[i - k] == 'e' || s[i - k] == 'i' || s[i - k] == 'o' || s[i - k] == 'u') {
            vowelCount--;
        }
        if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i' || s[i] == 'o' || s[i] == 'u') {
            vowelCount++;
        }
        maxVowelCount = max(maxVowelCount, vowelCount);  // update the maximum vowel count if the current count is higher
    }
    return maxVowelCount;  // return the maximum vowel count
}
```
{% endcode %}

The idea behind this algorithm is to use a sliding window to iterate over all substrings of length k in the input string s. For each substring, we count the number of vowels and update the maximum vowel count if the current count is higher. We start by counting the number of vowels in the first k characters, and then slide the window one character to the right and count the number of vowels in the new substring. We update the vowel count by subtracting the number of vowels in the character that was removed from the window and adding the number of vowels in the new character that was added to the window. We keep track of the maximum vowel count seen so far and return it at the end.

this solution is optimized as it has a time complexity of O(n), where n is the length of the input string s.

The algorithm uses a sliding window approach to iterate over all substrings of length k in the input string s. This allows us to count the number of vowels in each substring in constant time. We only need to count the number of vowels in the first k characters of s, and then slide the window one character at a time and update the vowel count in constant time for each new substring.

Overall, the time complexity of this algorithm is O(n) because we only need to iterate over the input string s once and the cost of counting vowels for each substring is constant time. Therefore, this is an optimized solution for this problem.
