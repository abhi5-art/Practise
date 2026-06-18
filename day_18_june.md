##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List
---

# DSA Problems Solved 

## Problem 1: Delete Node in a Linked List

### 🔹 Topic
- Linked List

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Since access to the head of the linked list was not provided, direct deletion of the current node was not possible.
- Copied the value of the next node into the given node.
- Updated the `next` pointer of the current node to skip the next node and point to the node after it.
- This effectively removed the next node from the linked list while making the current node appear deleted.

### 🔹 Time Complexity
- O(1)

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Singly Linked List
- Pointer Manipulation
- In-Place Modification


### Solution
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```

## Problem 2: Delete Nodes From Linked List Present in Array

### 🔹 Topic
- Linked List
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Stored all elements of the given array in a set for efficient lookup.
- Created a dummy node to simplify construction of the resulting linked list.
- Traversed the original linked list node by node.
- For each node:
  - Checked whether its value was present in the set.
  - If the value was not present, created a new node with that value and appended it to the result list.
  - Otherwise, skipped the node.
- Returned the linked list starting from `dummy->next`.

### 🔹 Time Complexity
- O(n log m)
  - `m` = size of `nums`
  - `n` = number of nodes in the linked list
  - Set insertion takes `O(log m)` and each lookup takes `O(log m)`.

### 🔹 Space Complexity
- O(m + n)
  - `O(m)` for the set.
  - `O(n)` for the newly created linked list in the worst case.

### 🔹 Concepts Used
- Singly Linked List
- Set STL
- Dummy Node
- Filtering Elements

### Solution
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* modifiedList(vector<int>& nums, ListNode* head) {
        set<int>st;
        for(auto x:nums)st.insert(x);

        ListNode* dummy = new ListNode(-1);
        ListNode* temp=dummy;

        ListNode* t=head;
        while(t){
            if(!st.count(t->val)){
                temp->next=new ListNode(t->val);
                temp=temp->next;
            }
            t=t->next;
        }

        return dummy->next;
    }
};
```