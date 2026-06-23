##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List(slow-fast Pointer)
---

# DSA Problems Solved 

## Problem 1: Linked List Cycle

### 🔹 Topic
- Linked List
- Two Pointers (Floyd's Cycle Detection)

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Handled edge cases where the linked list was empty or contained only one node.
- Used two pointers moving at different speeds:
  - `left` (slow pointer) moves one node at a time.
  - `right` (fast pointer) moves two nodes at a time.
- Initialized a dummy node before the head and positioned the pointers accordingly.
- Traversed the linked list while advancing both pointers.
- If the slow and fast pointers ever pointed to the same node, a cycle existed in the linked list.
- If the fast pointer reached the end of the list, no cycle was present.

### 🔹 Time Complexity
- O(n)
  - In the worst case, each node is visited a constant number of times.

### 🔹 Space Complexity
- O(1)
  - Only a few pointer variables are used.

### 🔹 Concepts Used
- Floyd's Cycle Detection Algorithm
- Fast and Slow Pointers
- Linked List Traversal
- Cycle Detection

### Solution
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head || !head->next)return false;
        
        //optimized 2 pointer
        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* left=dummy;
        ListNode* right=head;
        while(right){
            if(left == right)return true;

            left=left->next;
            right=right->next;
            if(right)right=right->next;
        }
        return false;
    }
};
```


## Problem 2: Linked List Cycle II

### 🔹 Topic
- Linked List
- Two Pointers (Floyd's Cycle Detection)

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Handled edge cases where the linked list was empty or contained only one node.
- Used Floyd's Cycle Detection Algorithm with two pointers:
  - `left` (slow pointer) moved one step at a time.
  - `right` (fast pointer) moved two steps at a time.
- Traversed the linked list until the two pointers met, indicating the presence of a cycle.
- Once a meeting point was found:
  - Reset the slow pointer to the head of the linked list.
  - Kept the fast pointer at the meeting point.
- Moved both pointers one step at a time.
- The node where they met again was the starting node of the cycle.
- If the fast pointer reached the end of the list, returned `NULL` since no cycle existed.

### 🔹 Time Complexity
- O(n)
  - One traversal to detect the cycle and another traversal to locate the cycle's starting node.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Floyd's Cycle Detection Algorithm
- Fast and Slow Pointers
- Cycle Detection
- Cycle Entry Point Detection
- Linked List Traversal

### Solution
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if(!head || !head->next)return NULL;

        ListNode* left=head;
        ListNode* right=head;
        while(right){
            left=left->next;
            right=right->next;
            if(right)right=right->next;

             if(left==right){
                left=head;
                break;
            }
        }
        if(!right)return NULL;
        
        while(left && right){
            if(left==right)return left;
            left=left->next;
            right=right->next;
        }
       
       return NULL;
    }
};
```