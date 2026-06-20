##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List Reversal
---

# DSA Problems Solved 

## Problem 1: Reverse Linked List I

### 🔹 Topic
- Linked List
- Pointer Manipulation

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used three pointers: `prev`, `curr`, and `next` to reverse the links of the linked list.
- Started with `prev` as `NULL` and `curr` pointing to the head.
- For each node:
  - Stored the next node using `next`.
  - Reversed the current node's link by pointing it to `prev`.
  - Moved `prev` and `curr` one step forward.
- Continued until all nodes were processed.
- Returned `prev`, which became the new head of the reversed linked list.

### 🔹 Time Complexity
- O(n)
  - Each node is visited exactly once.

### 🔹 Space Complexity
- O(1)
  - Reversal is performed in-place without using extra data structures.

### 🔹 Concepts Used
- Singly Linked List
- Pointer Manipulation
- Iterative Reversal
- In-Place Modification

### Solution
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* curr=head;
        ListNode* prev=NULL;
        ListNode* next=NULL;
        while(curr){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
};
```

## Problem 2: Reverse Linked List II

### 🔹 Topic
- Linked List
- Linked List Reversal
- Pointer Manipulation

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Handled the special case where `left == right`, as no reversal was required.
- Traversed the linked list to locate:
  - The node just before the reversal segment (`before_left`).
  - The starting node of the reversal segment (`left_node`).
- Used a helper function to reverse the linked list from position `left` to `right`.
- The helper function returned:
  - The head of the reversed sublist.
  - The node immediately after the reversed segment.
- Reconnected the reversed portion with the remaining linked list:
  - Connected `before_left` to the new head of the reversed sublist.
  - Connected the original `left_node` (which became the tail after reversal) to the node after the reversed segment.
- If the reversal started from the head (`left == 1`), returned the new head of the reversed sublist.
- Otherwise, returned the original head.

### 🔹 Time Complexity
- O(n)
  - The linked list is traversed once to locate the reversal boundaries and once more during reversal.

### 🔹 Space Complexity
- O(1)
  - Reversal is performed in-place using pointers.

### 🔹 Concepts Used
- Linked List Reversal
- Sublist Reversal
- Pointer Manipulation
- In-Place Modification
- Edge Case Handling

### Solution
```cpp
class Solution {
    vector<ListNode*> rev(ListNode* head, int position, int right){
        ListNode* curr=head;
        ListNode* prev=NULL;
        ListNode* next=NULL;
        
        vector<ListNode*>ans(2);
        while(curr){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
            if(position == right){
                ans[1]=curr;
                break;
            }
            position++;
        }
        ans[0]=prev;
        return ans;
    }
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if(left==right)return head;//edge case

        ListNode* temp=head;
        ListNode *before_left=NULL, *left_node=NULL, *after_right=NULL, *prev=NULL;
        int pos=1;
         
        while(temp){
            if(pos==left){
               left_node=temp;
               vector<ListNode*>t(2);
               t=rev(temp,left,right);
               prev=t[0];
               after_right=t[1];
               break;
            }else if(pos==left-1){
                before_left=temp;
            }
            temp=temp->next;
            pos++;
        }

        if(before_left)before_left->next = prev;//edge case
        left_node->next = after_right;
          
        if(left==1)return prev;//edge case

        return head;
    }
};
```