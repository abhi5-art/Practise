##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List(slow-fast Pointer)
---

# DSA Problems Solved 

## Problem 1: Delete the Middle Node of a Linked List

### 🔹 Topic
- Linked List
- Two Pointers

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Handled the edge case where the linked list contained only one node by returning `NULL`.
- Created a dummy node before the head to simplify deletion operations.
- Used two pointers:
  - `left` (slow pointer) moved one step at a time.
  - `right` (fast pointer) moved two steps at a time.
- When the fast pointer reached the end of the list, the slow pointer was positioned just before the middle node.
- Stored the middle node in a temporary pointer.
- Updated the slow pointer's `next` link to skip the middle node.
- Deleted the middle node and returned the modified linked list.

### 🔹 Time Complexity
- O(n)
  - The linked list is traversed only once.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Fast and Slow Pointers
- Linked List Traversal
- Node Deletion
- Dummy Node
- Pointer Manipulation

### Solution
```cpp
class Solution {
public:
    ListNode* deleteMiddle(ListNode* head) {
        if(!head->next)return NULL;//edge case

        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* left=dummy;
        ListNode* right=head;
        
        while(right && right->next){
            left=left->next;
            right=right->next;
            right=right->next;          
        }
        ListNode* temp=left->next;
        left->next=temp->next;
        delete temp;

        return head;
    }
};
```

## Problem 2: Remove Nth Node From End of List

### 🔹 Topic
- Linked List
- Two Pointers

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Handled the edge case where the linked list contained only one node by returning `NULL`.
- Created a dummy node before the head to simplify deletion operations, especially when the head node needed to be removed.
- Used two pointers:
  - `right` pointer was moved `n` steps ahead.
  - `left` pointer started from the dummy node.
- After creating a gap of `n` nodes, moved both pointers simultaneously until the `right` pointer reached the end of the list.
- At this point, the `left` pointer was positioned just before the node that needed to be deleted.
- Stored the target node in a temporary pointer.
- Updated the links to skip the target node and removed it from the list.
- Returned `dummy->next` as the head of the modified linked list.

### 🔹 Time Complexity
- O(n)
  - The linked list is traversed at most once.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Two Pointer Technique
- Fast and Slow Pointers
- Linked List Traversal
- Node Deletion
- Dummy Node
- Pointer Manipulation

### Solution
```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(!head->next)return NULL;

        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* left=dummy;
        ListNode* right=head;
        while(n && right){
            right=right->next;
            n--;
        }
        while(right){
            left=left->next;
            right=right->next;
        }
        ListNode* temp=left->next;
        left->next=temp->next;
        delete temp;

        return dummy->next;
    }
};
```