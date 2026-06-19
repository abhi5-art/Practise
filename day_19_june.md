##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List
---

# DSA Problems Solved 

## Problem 1: Remove Linked List Elements

### 🔹 Topic
- Linked List
- Pointer Manipulation

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Created a dummy node and connected it to the head of the linked list.
- Used a pointer to traverse the list starting from the dummy node.
- Checked the value of the next node at each step.
- If the next node contained the target value, updated the current node's `next` pointer to skip that node.
- Otherwise, moved the pointer forward.
- Using a dummy node simplified handling cases where the head node itself needed to be removed.
- Returned `dummy->next` as the head of the modified linked list.

### 🔹 Time Complexity
- O(n)
  - Each node is visited at most once.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Singly Linked List
- Dummy Node
- Pointer Manipulation
- Node Deletion

### Solution
```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* temp=dummy;

        while(temp->next){
            if(temp->next->val == val)temp->next=temp->next->next;
            else temp=temp->next;
        }

        return dummy->next;
    }
};
```

## Problem 2: Remove Nodes From Linked List

### 🔹 Topic
- Linked List
- Reversal Technique
- Greedy

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that a node should be removed if there exists a greater value on its right side.
- Reversed the linked list so that nodes could be processed from right to left.
- Maintained the maximum value encountered so far while traversing the reversed list.
- For each node:
  - If the next node's value was smaller than the current maximum, removed it from the list.
  - Otherwise, kept the node and updated the maximum value.
- After processing all nodes, reversed the linked list again to restore the original order.
- Returned the modified linked list.

### 🔹 Time Complexity
- O(n)
  - One traversal for each reversal and one traversal for node removal.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Linked List Reversal
- Greedy Observation
- Pointer Manipulation
- In-Place Modification

### Solution
```cpp
class Solution {
    ListNode* rev(ListNode* head){
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
public:
    ListNode* removeNodes(ListNode* head) {
        ListNode* h=rev(head);
        ListNode* temp=h;
        int maxi=temp->val;
        while(temp->next){
            if(temp->next->val < maxi)temp->next=temp->next->next;
            else temp=temp->next;
            maxi=max(maxi,temp->val);
        }
        ListNode* ans=rev(h);
        return ans;
    }
};
```