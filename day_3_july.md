##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Sliding Window
---

# DSA Problems Solved 

## Problem 1: Binary Tree Preorder Traversal

### 🔹 Topic
- Binary Tree
- Depth First Search (DFS)
- Recursion

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used recursion to perform a preorder traversal of the binary tree.
- If the current node was `NULL`, returned immediately.
- Visited the current node first and stored its value.
- Recursively traversed the left subtree.
- Recursively traversed the right subtree.
- Returned the traversal stored in the answer vector.

### 🔹 Time Complexity
- O(n)
  - Every node is visited exactly once.

### 🔹 Space Complexity
- O(h)
  - `h` is the height of the tree due to the recursion stack.
  - Worst case: `O(n)`, Best case (balanced tree): `O(log n)`.

### 🔹 Concepts Used
- Binary Tree
- DFS
- Preorder Traversal
- Recursion

### Solution
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
     vector<int>ans;
    void pre(TreeNode* root){
         if(root==NULL){
            return ;
        }
        ans.push_back(root->val);
        pre(root->left);
        pre(root->right);
    }
public:
    vector<int> preorderTraversal(TreeNode* root) {
        pre(root);
        return ans;
    }
};
```


## Problem 2: Binary Tree Inorder Traversal

### 🔹 Topic
- Binary Tree
- Depth First Search (DFS)
- Recursion

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used recursion to perform an inorder traversal of the binary tree.
- If the current node was `NULL`, returned immediately.
- Recursively traversed the left subtree.
- Visited the current node and stored its value.
- Recursively traversed the right subtree.
- Returned the traversal stored in the answer vector.

### 🔹 Time Complexity
- O(n)
  - Every node is visited exactly once.

### 🔹 Space Complexity
- O(h)
  - `h` is the height of the tree due to the recursion stack.
  - Worst case: `O(n)`, Best case (balanced tree): `O(log n)`.

### 🔹 Concepts Used
- Binary Tree
- DFS
- Inorder Traversal
- Recursion


### Solution
```cpp
class Solution {
     vector<int>ans;
    void inorder(TreeNode* root){
         if(root==NULL){
            return ;
        }
        inorder(root->left);
        ans.push_back(root->val);
        inorder(root->right);
    }
public:
    
    vector<int> inorderTraversal(TreeNode* root) {
       inorder(root);
       return ans;
    }
};
```


## Problem 3: Binary Tree Postorder Traversal

### 🔹 Topic
- Binary Tree
- Depth First Search (DFS)
- Recursion

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used recursion to perform a postorder traversal of the binary tree.
- If the current node was `NULL`, returned immediately.
- Recursively traversed the left subtree.
- Recursively traversed the right subtree.
- Visited the current node and stored its value.
- Returned the traversal stored in the answer vector.

### 🔹 Time Complexity
- O(n)
  - Every node is visited exactly once.

### 🔹 Space Complexity
- O(h)
  - `h` is the height of the tree due to the recursion stack.
  - Worst case: `O(n)`, Best case (balanced tree): `O(log n)`.

### 🔹 Concepts Used
- Binary Tree
- DFS
- Postorder Traversal
- Recursion


### Solution
```cpp
class Solution {
     vector<int>ans;
    void post(TreeNode* root){
         if(root==NULL){
            return ;
        }
        post(root->left);
        post(root->right);
        ans.push_back(root->val);

    }
public:
    vector<int> postorderTraversal(TreeNode* root) {
        post(root);
        return ans;
    }
};
```
