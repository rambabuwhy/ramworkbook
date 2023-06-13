# Snippets-part 2

1. sort():

Sorts a range of elements in ascending or descending order.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
sort(v.begin(), v.end()); // Sort the vector in ascending order
```

2. reverse():

Reverses the order of elements in a range.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
reverse(v.begin(), v.end()); // Reverse the order of elements in the vector
```

3. min\_element():

Returns an iterator to the smallest element in a range.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
auto smallest = min_element(v.begin(), v.end()); // Find the smallest element in the vector
```

4. max\_element():

Returns an iterator to the largest element in a range.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
auto largest = max_element(v.begin(), v.end()); // Find the largest element in the vector
```

5. count():

Returns the number of occurrences of a value in a range.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
int count_of_5 = count(v.begin(), v.end(), 5); // Count the number of occurrences of 5 in the vector
```

6. accumulate():

Returns the sum of all elements in a range.

```cpp
#include <numeric>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
int sum = accumulate(v.begin(), v.end(), 0); // Compute the sum of elements in the vector
```

7. next\_permutation():

Rearranges the elements in a range into the next lexicographically greater permutation.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4};
do {
    // Do something with the permutation
} while (next_permutation(v.begin(), v.end())); // Iterate over all permutations of the vector
```

8. prev\_permutation():

Rearranges the elements in a range into the next lexicographically smaller permutation.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {4, 1, 3};
do {
    // Do something with the permutation
} while (prev_permutation(v.begin(), v.end())); // Iterate over all permutations of the vector in reverse order
```

9. binary\_search():

Determines whether a value exists in a sorted range.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {1, 3, 4, 5, 7, 9};
bool found = binary_search(v.begin(), v.end(), 4); // Check if 4 exists in the vector
```

10. lower\_bound():

Finds the iterator to the first element in a sorted range that is greater than or equal to a given value.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {1, 3, 4, 5, 7, 9};
auto it = lower_bound(v.begin(), v.end(), 6); // Find the first element in the vector that is greater than or equal to 6
```

11. upper\_bound():

Finds the iterator to the first element in a sorted range that is greater than a given value.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {1, 3, 4, 5, 7, 9};
auto it = upper_bound(v.begin(), v.end(), 6); // Find the first element in the vector that is greater than 6
```

12. set\_intersection():

Computes the intersection of two sorted ranges.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v1 = {1, 3, 4, 5, 7, 9};
vector<int> v2 = {2, 3, 5, 6, 8};
vector<int> v_intersection;
set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), back_inserter(v_intersection)); // Compute the intersection of v1 and v2 and store the result in v_intersection
```

13. set\_union():

Computes the union of two sorted ranges.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v1 = {1, 3, 4, 5, 7, 9};
vector<int> v2 = {2, 3, 5, 6, 8};
vector<int> v_union;
set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), back_inserter(v_union)); // Compute the union of v1 and v2 and store the result in v_union
```

14. set\_difference():

Computes the difference of two sorted ranges.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v1 = {1, 3, 4, 5, 7, 9};
vector<int> v2 = {2, 3, 5, 6, 8};
vector<int> v_difference;
set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), back_inserter(v_difference)); // Compute the difference of v1 and v2 and store the result in v_difference
```

15. nth\_element():

Rearranges the elements in a range such that the nth element is in its sorted position.

```cpp
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
nth_element(v.begin(), v.begin() + 4, v.end()); // Rearrange the elements in the v
```

16. find():

Returns the iterator to the first occurrence of a value in a range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 2, 3, 5, 7, 11 };

    // Find the iterator to the first occurrence of 5
    auto it = std::find(v.begin(), v.end(), 5);

    // Print the value pointed to by the iterator
    std::cout << *it << std::endl; // Output: 5

    return 0;
}
```

17. fill():

Assigns a given value to all elements in a range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v(10);

    // Fill the vector with the value 42
    std::fill(v.begin(), v.end(), 42);

    // Print the contents of the vector
    for (auto i : v) {
        std::cout << i << " "; // Output: 42 42 42 42 42 42 42 42 42 42
    }
    std::cout << std::endl;

    return 0;
}
```

18. copy():

Copies elements from one range to another.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v1 { 2, 3, 5, 7, 11 };
    std::vector<int> v2(5);

    // Copy the contents of v1 to v2
    std::copy(v1.begin(), v1.end(), v2.begin());

    // Print the contents of v2
    for (auto i : v2) {
        std::cout << i << " "; // Output: 2 3 5 7 11
    }
    std::cout << std::endl;

    return 0;
}
```

19. unique():

Removes consecutive duplicate elements from a range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 2, 2, 3, 3, 5, 7, 7, 7, 11 };

    // Remove consecutive duplicates
    auto last = std::unique(v.begin(), v.end());
    v.erase(last, v.end());

    // Print the contents of the vector
    for (auto i : v) {
        std::cout << i << " "; // Output: 2 3 5 7 11
    }
    std::cout << std::endl;

    return 0;
}
```

20. &#x20;distance():

Computes the distance between two iterators.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 2, 3, 5, 7, 11 };

    // Compute the distance between the beginning and end of v
    auto dist = std::distance(v.begin(), v.end());

    // Print the distance
    std::cout << dist << std::endl; // Output: 5

    return 0;
}
```

21. rotate():&#x20;

Rotates the order of elements in a range by a specified number of positions.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 1, 2, 3, 4, 5 };

    // Rotate the elements of v by 2 positions to the left
    std::rotate(v.begin(), v.begin() + 2, v.end());

    // Print the contents of the vector
    for (auto i : v) {
        std::cout << i << " "; // Output: 3 4 5 1 2
    }
    std::cout << std::endl;

    return 0;
}
```

22. &#x20;partition():

Rearranges the elements in a range so that all elements that satisfy a predicate come before those that do not.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5 };

    // Rearrange the elements of v so that even numbers come before odd numbers
    auto pivot = std::partition(v.begin(), v.end(), [](int i) { return i % 2 == 0; });

    // Print the contents of the vector
    for (auto i : v) {
        std::cout << i << " "; // Output: 4 2 6 3 1 5 9 5 3 5 1
    }
    std::cout << std::endl;

    return 0;
}
```

23. &#x20;merge():

Merges two sorted ranges into a single sorted range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v1 { 2, 4, 6, 8 };
    std::vector<int> v2 { 1, 3, 5, 7 };

    // Merge the two sorted vectors into a single sorted vector
    std::vector<int> v3(v1.size() + v2.size());
    std::merge(v1.begin(), v1.end(), v2.begin(), v2.end(), v3.begin());

    // Print the contents of the vector
    for (auto i : v3) {
        std::cout << i << " "; // Output: 1 2 3 4 5 6 7 8
    }
    std::cout << std::endl;

    return 0;
}
```

24. &#x20;minmax\_element():

Returns a pair of iterators to the smallest and largest elements in a range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 2, 3, 5, 7, 11 };

    // Get the iterators to the smallest and largest elements of v
    auto [min_it, max_it] = std::minmax_element(v.begin(), v.end());

    // Print the values pointed to by the iterators
    std::cout << *min_it << " " << *max_it << std::endl; // Output: 2 11

    return 0;
}
```

25. &#x20;clamp():

Restricts a value to a specified range.

```cpp
#include <algorithm>
#include <iostream>

int main() {
    int x = 5;

    // Restrict x to the range [1, 10]
    x = std::clamp(x, 1, 10);

    // Print the value of x
    std::cout << x << std::endl; // Output: 5

    return 0;
}
```

26. swap():

Swaps the values of two objects.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    int a = 5;
    int b = 10;

    // Swap the values of a and b
    std::swap(a, b);

    // Print the values of a and b
    std::cout << a << " " << b << std::endl; // Output: 10 5

    return 0;
}
```

27. shuffle():

Randomly shuffles the elements in a range.

```cpp
#include <algorithm>
#include <vector>
#include <random>
#include <iostream>

int main() {
    std::vector<int> v { 1, 2, 3, 4, 5 };

    // Shuffle the elements of v randomly
    std::random_device rd;
    std::mt19937 g(rd());
    std::shuffle(v.begin(), v.end(), g);

    // Print the contents of the vector
    for (auto i : v) {
        std::cout << i << " "; // Output: (random order)
    }
    std::cout << std::endl;

    return 0;
}
```

28. &#x20;count():

Counts the number of occurrences of a value in a range.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 1, 2, 3, 2, 1 };

    // Count the number of occurrences of the value 2 in v
    int count = std::count(v.begin(), v.end(), 2);

    // Print the result
    std::cout << count << std::endl; // Output: 2

    return 0;
}
```

29. &#x20;count\_if():

Counts the number of elements in a range that satisfy a given condition.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 1, 2, 3, 4, 5 };

    // Count the number of even numbers in v
    int count = std::count_if(v.begin(), v.end(), [](int i) { return i % 2 == 0; });

    // Print the result
    std::cout << count << std::endl; // Output: 2

    return 0;
}
```

30. &#x20;all\_of():

Returns true if all elements in a range satisfy a given condition.

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v { 2, 4, 6, 8 };

    // Check if all elements of v are even
    bool all_even = std::all_of(v.begin(), v.end(), [](int i) { return i % 2 == 0; });

    // Print the result
    std::cout << std::boolalpha << all_even << std::endl; // Output: true

    return 0;
}
```
