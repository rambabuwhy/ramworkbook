# Minimum Absolute Difference in a Binary Search Tree

## Problem:

Given the root of a Binary Search Tree (BST), find the minimum absolute difference between the values of any two different nodes in the tree.

A Binary Search Tree is a binary tree in which for each node, the value of all the nodes in its left subtree is less than its value, and the value of all the nodes in its right subtree is greater than its value.

**Function Signature:**

```cpp
cppCopy codeint getMinimumDifference(TreeNode* root);
```

**Input:**

* The input parameter `root` is a pointer to the root node of a BST.

**Output:**

* The function should return an integer, which represents the minimum absolute difference between the values of any two different nodes in the BST.

**Example:**

```cpp
        4
       / \
      2   6
     / \
    1   3
```

Input: `root = [4, 2, 6, 1, 3]` Output: `1` Explanation: The minimum absolute difference occurs between the nodes with values 3 and 4, resulting in an absolute difference of 1.

**Note:**

* The given BST will have at least two nodes.
* The values of the BST nodes are unique.

## Solution:

Here's a breakdown of your code:

```cpp
int val = -1;
int diff = INT_MAX;

int getMinimumDifference(TreeNode* root) {
    if (root->left != NULL) {
        getMinimumDifference(root->left);
    }
    
    if (val >= 0) {
        diff = min(diff, root->val - val);
    }
    val = root->val;
    
    if (root->right != NULL) {
        getMinimumDifference(root->right);
    }
    
    return diff;
}
```

The variables `val` and `diff` are used to keep track of the previous node's value and the minimum absolute difference respectively. The function recursively traverses the BST in an in-order manner.

1. If the left child of the current node exists, the function is called recursively for the left subtree.
2. After visiting the left subtree, if `val` is greater than or equal to 0, it means that a previous node has been visited. In this case, the difference between the current node's value (`root->val`) and the previous node's value (`val`) is calculated and compared with the current minimum difference (`diff`). If the new difference is smaller, it replaces the current minimum difference.
3. The `val` variable is updated with the current node's value for the next iteration.
4. If the right child of the current node exists, the function is called recursively for the right subtree.
5. Finally, the minimum difference (`diff`) is returned as the result.

Overall, your code correctly calculates the minimum absolute difference between the values of any two different nodes in the BST using an in-order traversal approach.

Note:&#x20;

The provided code is not optimized because it uses a global variable (`val`) to keep track of the previous node's value. This approach can lead to incorrect results if the function is called multiple times for different BSTs concurrently. Additionally, using a global variable violates the principle of encapsulation and can introduce bugs in more complex code.

To optimize the solution, we can modify the in-order traversal approach by using a stack or iterative traversal instead of recursion. This allows us to eliminate the need for a global variable and achieve the same result more efficiently.

```cpp
#include <climits>
#include <stack>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int getMinimumDifference(TreeNode* root) {
    std::stack<TreeNode*> stk;
    TreeNode* curr = root;
    TreeNode* prev = nullptr;
    int minDiff = INT_MAX;

    while (curr != nullptr || !stk.empty()) {
        while (curr != nullptr) {
            stk.push(curr);
            curr = curr->left;
        }

        curr = stk.top();
        stk.pop();

        if (prev != nullptr)
            minDiff = std::min(minDiff, curr->val - prev->val);

        prev = curr;
        curr = curr->right;
    }

    return minDiff;
}

```

This optimized code uses an iterative in-order traversal using a stack. It starts from the root and traverses all the left children until reaching the leftmost node. It then processes the current node, compares the difference with the previous node, updates the minimum difference if necessary, and moves to the right child. The process continues until all nodes are processed.

By avoiding recursion and utilizing a stack for iterative traversal, we eliminate the need for a global variable and achieve better efficiency.
