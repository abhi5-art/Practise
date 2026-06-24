##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Linked-List
---

# DSA Problems Solved 

## Problem 1: Add Two Numbers I

### 🔹 Topic
- Linked List
- Simulation
- Mathematics

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Traversed both linked lists simultaneously, treating each node as a digit of a number stored in reverse order.
- Maintained a `carry` variable to handle sums greater than 9.
- For each pair of nodes:
  - Added their values along with the carry.
  - Created a new node containing `sum % 10`.
  - Updated the carry as `sum / 10`.
- After one list ended, continued processing the remaining nodes of the other list while considering the carry.
- If a carry remained after processing all nodes, created an additional node to store it.
- Used a dummy node to simplify construction of the result linked list.
- Returned `dummy->next` as the head of the final sum list.

### 🔹 Time Complexity
- O(max(n, m))
  - Each node from both linked lists is processed exactly once.

### 🔹 Space Complexity
- O(max(n, m))
  - A new linked list is created to store the result.

### 🔹 Concepts Used
- Linked List Traversal
- Carry Handling
- Digit-by-Digit Addition
- Dummy Node
- Simulation

### Solution
```cpp
class Solution {

public:

    ListNode* addTwoNumbers(ListNode* h1, ListNode* h2) {

        ListNode* t1=h1;

        ListNode* t2=h2;

        ListNode* dummy=new ListNode(-1);

        ListNode* temp=dummy;

        int sum,carry=0;

        while(t1 && t2){

            sum=t1->val+t2->val;

            sum+=carry;

            temp->next=new ListNode(sum%10);

            temp=temp->next;

            if(sum > 9)carry=1;

            else carry=0;



            t1=t1->next;

            t2=t2->next;

        }

        while(t1){

            sum=t1->val+carry;

            temp->next=new ListNode(sum%10);

            temp=temp->next;

            if(sum > 9)carry=1;

            else carry=0;



            t1=t1->next;

        }

        while(t2){

            sum=t2->val+carry;

            temp->next=new ListNode(sum%10);

            temp=temp->next;

            if(sum > 9)carry=1;

            else carry=0;



            t2=t2->next;

        }    

        if(carry==1){

            temp->next=new ListNode(1);

        }

        

        return dummy->next;

    }

};
```

## Problem 2: Add Two Numbers II

### 🔹 Topic
- Linked List
- Linked List Reversal
- Mathematics

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that the digits were stored in forward order, making direct addition difficult.
- Reversed both linked lists so that addition could be performed from the least significant digit.
- Used a carry variable while traversing both reversed lists.
- Added corresponding digits along with the carry and created new nodes containing `sum % 10`.
- Updated the carry as needed after each addition.
- Continued processing any remaining nodes from either list.
- If a carry remained after all digits were processed, added an extra node.
- Reversed the resulting linked list to restore the digits to forward order.
- Returned the head of the reversed result list.

### 🔹 Time Complexity
- O(n + m)
  - Both linked lists are reversed and traversed once.

### 🔹 Space Complexity
- O(max(n, m))
  - A new linked list is created to store the result.

### 🔹 Concepts Used
- Linked List Reversal
- Carry Handling
- Digit-by-Digit Addition
- Dummy Node
- Simulation
- Linked List Traversal

### Solution
```cpp
class Solution {
    ListNode* rev(ListNode* head){
        ListNode* curr=head;
        ListNode* next=NULL;
        ListNode* prev=NULL;

        while(curr){
            next=curr->next;
            curr->next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* t1=rev(l1);
        ListNode* t2=rev(l2);
        ListNode* dummy=new ListNode(-1);
        ListNode* temp=dummy;
        int sum,carry=0;
        while(t1 && t2){
            sum=t1->val+t2->val;
            sum+=carry;
            temp->next=new ListNode(sum%10);
            temp=temp->next;
            if(sum > 9)carry=1;
            else carry=0;

            t1=t1->next;
            t2=t2->next;
        }
        while(t1){
            sum=t1->val+carry;
            temp->next=new ListNode(sum%10);
            temp=temp->next;
            if(sum > 9)carry=1;
            else carry=0;

            t1=t1->next;
        }
        while(t2){
            sum=t2->val+carry;
            temp->next=new ListNode(sum%10);
            temp=temp->next;
            if(sum > 9)carry=1;
            else carry=0;

            t2=t2->next;
        }    
        if(carry==1){
            temp->next=new ListNode(1);
        }
        
        ListNode* ans=rev(dummy->next);

        return ans;
    }
};
```

