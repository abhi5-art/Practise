##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List(slow-fast Pointer)
---

# DSA Problems Solved 

## Problem 1: Middle of the Linked List

### 🔹 Topic
- Linked List
- Two Pointers

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used two pointers moving at different speeds:
  - `left` pointer moved one node at a time.
  - `right` pointer moved two nodes at a time.
- Initialized a dummy node before the head to simplify handling of even-length lists.
- Counted the total number of nodes traversed by the fast pointer.
- When the fast pointer reached the end of the list, the slow pointer was positioned near the middle.
- For odd-length lists, returned the node pointed to by `left`.
- For even-length lists, returned `left->next` to satisfy the requirement of returning the second middle node.

### 🔹 Time Complexity
- O(n)
  - The linked list is traversed only once.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Fast and Slow Pointers
- Linked List Traversal
- Middle Element Detection
- Edge Case Handling

### Solution
```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* left=dummy;
        ListNode* right=head;
        int cnt=0;
        while(right){
            left=left->next;
            right=right->next;
            cnt++;
            if(right){
                right=right->next;
                cnt++;
            }
        }
        if(cnt%2==0)return left->next;
        
        return left; 
    }
};
```

## Problem 2: Palindrome Linked List

### 🔹 Topic
- Linked List
- Two Pointers
- Linked List Reversal

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used the fast and slow pointer technique to locate the middle of the linked list.
- Moved the slow pointer one step at a time and the fast pointer two steps at a time.
- After reaching the middle, moved the slow pointer to the start of the second half of the list.
- Reversed the second half of the linked list using an iterative reversal function.
- Compared nodes from the beginning of the list and the reversed second half simultaneously.
- If any pair of corresponding nodes had different values, returned `false`.
- If all compared nodes matched, returned `true`, confirming that the linked list was a palindrome.

### 🔹 Time Complexity
- O(n)
  - One traversal to find the middle, one traversal to reverse the second half, and one traversal for comparison.

### 🔹 Space Complexity
- O(1)
  - Reversal and comparison are performed in-place using pointers.

### 🔹 Concepts Used
- Fast and Slow Pointers
- Linked List Reversal
- Two-Pointer Comparison
- In-Place Processing
- Palindrome Checking

### Solution
```cpp
class Solution {
    ListNode* rev(ListNode* head){
        ListNode* prev=NULL;
        ListNode* next=NULL;
        ListNode* curr=head;
        while(curr){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
public:
    bool isPalindrome(ListNode* head) {
        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* left=dummy;
        ListNode* right=head;

        while(right){
           left=left->next;
           right=right->next;
           if(right)right=right->next;
        }
        left=left->next;
        ListNode* rev_head=rev(left);
        
        ListNode* t1=head;
        ListNode* t2=rev_head;
        while(t2){
            if(t2->val != t1->val)return false;
            t1=t1->next;
            t2=t2->next;
        }
        return true;
    }
};
```