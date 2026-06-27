##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : String,stack
---

# DSA Problems Solved 

## Problem 1: Remove Outermost Parentheses

### 🔹 Topic
- Stack
- Strings

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used a stack to identify the outermost pair of parentheses in each primitive valid parentheses string.
- Stored the indices of opening parentheses in the stack.
- Whenever a closing parenthesis was encountered:
  - If the stack contained only one opening parenthesis, the current pair represented the outermost parentheses.
  - Stored the indices of both the opening and closing parentheses in a set and removed the opening parenthesis from the stack.
  - Otherwise, simply popped the matching opening parenthesis from the stack.
- After processing the entire string, traversed it once more and appended only those characters whose indices were not present in the set.
- Returned the resulting string after removing all outermost parentheses.

### 🔹 Time Complexity
- O(n log n)
  - Stack operations take `O(n)`.
  - Set insertion and lookup take `O(log n)`.

### 🔹 Space Complexity
- O(n)
  - Additional space is used for the stack and the set storing indices.

### 🔹 Concepts Used
- Stack
- Parentheses Matching
- Set STL
- Index Tracking
- String Traversal

### Solution
```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        int n=s.size();
        string ans="";
        set<int>temp;
        stack<int>st;

        for(int i=0;i<n;i++){
            if(s[i]=='('){
                st.push(i);
            }else{
                if(st.size() == 1){
                   temp.insert(st.top());
                   temp.insert(i);
                   st.pop();
                }else{
                    st.pop();
                }
            }
        }

        for(int i=0;i<n;i++){
            if(temp.find(i) == temp.end())ans+=s[i];
        }
        return ans;
    }
};
```



### Solution
```cpp

```
