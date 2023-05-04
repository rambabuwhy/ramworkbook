# snippets

1. Reading input from standard input:

Useful for reading input data from a file or writing output data to a file in competitive programming problems.

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;
    // read n from standard input
    return 0;
}
```
{% endcode %}

2. Reading input from a file:

{% code lineNumbers="true" %}
```cpp
#include <fstream>
using namespace std;

int main() {
    ifstream infile("input.txt");
    int n;
    infile >> n;
    // read n from input.txt
    infile.close();
    return 0;
}
```
{% endcode %}

3. Writing output to standard output:

This is useful for displaying results or messages to the user during runtime.

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    int n = 42;
    cout << n << endl;
    // write n to standard output followed by a newline
    return 0;
}

```
{% endcode %}

4. Writing output to a file:

{% code lineNumbers="true" %}
```cpp
using namespace std;

int main() {
    ofstream outfile("output.txt");
    int n = 42;
    outfile << n << endl;
    // write n to output.txt followed by a newline
    outfile.close();
    return 0;
}
```
{% endcode %}

5. Looping through an array:

{% code lineNumbers="true" %}
```cpp
using namespace std;

int main() {
    int a[] = {1, 2, 3, 4, 5};
    int n = sizeof(a) / sizeof(a[0]);
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    cout << endl;
    // output: 1 2 3 4 5
    return 0;
}
```
{% endcode %}

6. Sorting an array:

Sorting is a common operation in many algorithms, and these snippets show how to use the built-in sorting functions in C++.

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    int a[] = {5, 2, 1, 4, 3};
    int n = sizeof(a) / sizeof(a[0]);
    sort(a, a + n);
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    cout << endl;
    // output: 1 2 3 4 5
    return 0;
}
```
{% endcode %}

7. Using a vector:

Vectors are similar to arrays, but can dynamically resize themselves as needed, making them useful for situations where the size of the data set may change.

{% code lineNumbers="true" %}
```cpp
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;
    // output: 1 2 3
    return 0;
}
```
{% endcode %}

8. Using a map:

Useful for storing key-value pairs and quickly accessing values based on keys, which can be used to solve problems related to counting or mapping elements.

{% code lineNumbers="true" %}
```cpp
#include <map>
using namespace std;

int main() {
    map<string, int> m;
    m["Alice"] = 42;
    m["Bob"] = 24;
    cout << m["Alice"] << endl;
    // output: 42
    return 0;
}
```
{% endcode %}

9. Using a set:

Useful for storing a collection of elements and quickly checking whether an element is present or not, which can be used to solve problems related to finding distinct elements or removing duplicate

{% code lineNumbers="true" %}
```cpp
#include <set>
using namespace std;

int main() {
    set<int> s;
    s.insert(1);
    s.insert(2);
    s.insert(3);
    if (s.find(2) != s.end()) {
        cout << "2 is in the set" << endl;
    }
    // output: 2 is in the set
    return 0;
}
```
{% endcode %}

10. Using a queue:

Useful for storing and manipulating data in a First-In-First-Out (FIFO) fashion, which can be used to solve problems related to simulating real-world scenarios

{% code lineNumbers="true" %}
```cpp
#include <queue>
using namespace std;

int main() {
    queue<int> q;
    q.push(1);
    q.push(2);
    q.push(3);
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
    // output: 1 2 3
    return 0;
}
```
{% endcode %}

11. Using a stack:

Useful for storing and manipulating data in a Last-In-First-Out (LIFO) fashion, which can be used to solve problems related to checking whether a sequence of parentheses is balanced or not.

{% code lineNumbers="true" %}
```cpp
#include <stack>
using namespace std;

int main() {
    stack<int> s;
    s.push(1);
    s.push(2);
    s.push(3);
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
    // output: 3 2 1
    return 0;
}
```
{% endcode %}

12. Using a priority queue:

Useful for storing and manipulating data in a First-In-First-Out (FIFO) fashion, which can be used to solve problems related to simulating real-world scenarios.

{% code lineNumbers="true" %}
```cpp
#include <queue>
using namespace std;

int main() {
    priority_queue<int> pq;
    pq.push(3);
    pq.push(1);
    pq.push(2);
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;
    // output: 3 2 1
    return 0;
}
```
{% endcode %}

13. Binary search:

Useful for finding a specific element in a sorted array or vector, which can be used to solve various problems in competitive programming

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    int a[] = {1, 2, 3, 4, 5};
    int n = sizeof(a) / sizeof(a[0]);
    if (binary_search(a, a + n, 3)) {
        cout << "3 is in the array" << endl;
    }
    // output: 3 is in the array
    return 0;
}
```
{% endcode %}

14. Finding the minimum/maximum element:

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    int a[] = {5, 2, 1, 4, 3};
    int n = sizeof(a) / sizeof(a[0]);
    int min_elem = *min_element(a, a + n);
    int max_elem = *max_element(a, a + n);
    cout << "min = " << min_elem << ", max = " << max_elem << endl;
    // output: min = 1, max = 5
    return 0;
}
```
{% endcode %}

15. Reversing a string:

Useful for solving problems related to parsing or processing strings, which are often present in competitive programming problems.

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    string s = "hello";
    reverse(s.begin(), s.end());
    cout << s << endl;
    // output: olleh
    return 0;
}
```
{% endcode %}

16. Splitting a string:

Useful for solving problems related to parsing or processing strings, which are often present in competitive programming problems.

{% code lineNumbers="true" %}
```cpp
#include <sstream>
#include <vector>
using namespace std;

int main() {
    string s = "1 2 3 4 5";
    vector<int> v;
    istringstream iss(s);
    int x;
    while (iss >> x) {
        v.push_back(x);
    }
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;
    // output: 1 2 3 4 5
    return 0;
}
```
{% endcode %}

17. Getting the current time:

Useful for measuring the running time of programs or calculating time-based values in competitive programming problems.

{% code lineNumbers="true" %}
```cpp
#include <iostream>
using namespace std;

int main() {
    auto now = chrono::system_clock::now();
    time_t t = chrono::system_clock::to_time_t(now);
    cout << ctime(&t) << endl;
    // output: current date and time
    return 0;
}
```
{% endcode %}

18. Finding the gcd/lcm:

Useful for finding the greatest common divisor or least common multiple of two numbers, which can be used to solve problems related to number theory or modular arithmetic.

{% code lineNumbers="true" %}
```cpp
#include <numeric>
using namespace std;

int main() {
    int a = 12, b = 18;
    int gcd_val = gcd(a, b);
    int lcm_val = lcm(a, b);
    cout << "gcd = " << gcd_val << ", lcm = " << lcm_val << endl;
    // output: gcd = 6, lcm = 36
    return 0;
}
```
{% endcode %}

19. Generating random numbers:

Useful for generating random data or simulating stochastic processes in competitive programming problems.

{% code lineNumbers="true" %}
```cpp
#include <random>
using namespace std;

int main() {
    random_device rd;
    mt19937 gen(rd());
    uniform_int_distribution<> dis(1, 6);
    for (int i = 0; i < 10; i++) {
        cout << dis(gen) << " ";
    }
    cout << endl;
    // output: 3 5 1 2 5 2 5 2 5 5
    return 0;
}
```
{% endcode %}

20. Bit manipulation:

Useful for manipulating data at the bit level, which can be used to solve problems related to computer architecture or algorithms.

{% code lineNumbers="true" %}
```cpp
using namespace std;

int main() {
    int a = 5; // 101 in binary
    int b = 3; // 011 in binary
    int c = a & b; // 001 in binary
    int d = a | b; // 111 in binary
    int e = a ^ b; // 110 in binary
    int f = ~a; // 11111111111111111111111111111010 in binary (assuming 32-bit integers)
    int g = a << 1; // 1010 in binary
    int h = a >> 1; // 10 in binary
    cout << c << " " << d << " " << e << " " << f << " " << g << " " << h << endl;
    // output: 1 7 6 -6 10 2
    return 0;
}
```
{% endcode %}

21. Computing the factorial:

Useful for calculating the factorial of a number, which can be used to solve problems related to combinatorics.

{% code lineNumbers="true" %}
```cpp
using namespace std;

int main() {
    int n = 5;
    int fact = 1;
    for (int i = 1; i <= n; i++) {
        fact *= i;
    }
    cout << fact << endl;
    // output: 120
    return 0;
}
```
{% endcode %}

22. Computing the fibonacci sequence:

Useful for generating the fibonacci sequence up to a certain number of terms, which can be used to solve problems related to sequence generation or dynamic programming.

{% code lineNumbers="true" %}
```cpp
using namespace std;

int main() {
    int n = 10;
    int a = 0, b = 1, c;
    for (int i = 0; i < n; i++) {
        cout << a << " ";
        c = a + b;
        a = b;
        b = c;
    }
    cout << endl;
    // output: 0 1 1 2 3 5 8 13 21 34
    return 0;
}
```
{% endcode %}
