##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : String,stack
---

# DSA Problems Solved 

## Problem 1: Maximum Nesting Depth of the Parentheses

### 🔹 Topic
- Strings
- Stack Concept
- Parentheses

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Traversed the string character by character.
- Maintained a counter to represent the current nesting depth of parentheses.
- Incremented the counter whenever an opening parenthesis `'('` was encountered.
- Decremented the counter whenever a closing parenthesis `')'` was encountered.
- Updated the maximum depth after processing each character.
- Returned the maximum nesting depth found during the traversal.

### 🔹 Time Complexity
- O(n)
  - The string is traversed exactly once.

### 🔹 Space Complexity
- O(1)
  - Only two integer variables are used to track the current and maximum depth.

### 🔹 Concepts Used
- String Traversal
- Parentheses Matching
- Counter Technique
- Maximum Tracking

### Solution
```cpp
class Solution {
public:
    int maxDepth(string s) {
        int n=s.size();
        int cnt=0,ans=0;
        for(int i=0;i<n;i++){
            if(s[i]=='(')cnt++;
            else if(s[i]==')')cnt--;
            ans=max(ans,cnt);
        }
        return ans;
    }
};
```

## Problem 2: Backspace String Compare

### 🔹 Topic
- Strings
- Stack

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used two stacks to simulate typing for both input strings.
- Traversed each string character by character.
- If the current character was not `'#'`, pushed it onto the corresponding stack.
- If the current character was `'#'`, removed the top character from the stack if it was not empty, simulating the backspace operation.
- After processing both strings completely, compared the two stacks.
- Returned `true` if both stacks were identical; otherwise returned `false`.

### 🔹 Time Complexity
- O(n + m)
  - `n` and `m` are the lengths of the two input strings.

### 🔹 Space Complexity
- O(n + m)
  - In the worst case, both stacks may store all characters of the input strings.

### 🔹 Concepts Used
- Stack
- String Traversal
- Simulation
- Stack Comparison

### Solution
```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        stack<char>st1;
        stack<char>st2;
        for(auto x:s){
            if(x=='#'){
                if(!st1.empty())st1.pop();
            }
            else st1.push(x);
        }
        for(auto x:t){
            if(x=='#'){
                if(!st2.empty())st2.pop();
            }
            else st2.push(x);
        }

        return st1==st2;
    }
};
```

## Problem 3: Valid Parentheses

### 🔹 Topic
- Stack
- Strings

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used a stack to keep track of opening brackets encountered while traversing the string.
- Whenever an opening bracket (`(`, `{`, `[`) was found, pushed it onto the stack.
- For every closing bracket, checked whether the stack was non-empty and whether the top of the stack contained the corresponding opening bracket.
- If a valid matching pair was found, popped the opening bracket from the stack.
- If the stack was empty or the brackets did not match, returned `false`.
- After processing the entire string, returned `true` only if the stack was empty, indicating that all brackets were matched correctly.

### 🔹 Time Complexity
- O(n)
  - Each character is pushed to or popped from the stack at most once.

### 🔹 Space Complexity
- O(n)
  - In the worst case, all opening brackets are stored in the stack.

### 🔹 Concepts Used
- Stack
- Parentheses Matching
- String Traversal
- LIFO (Last In, First Out)

### Solution
```cpp
class Solution {
public:
    bool isValid(string s) {
        int n=s.size();
        stack<char>st;

        for(int i=0;i<n;i++){
            if(s[i]=='(' || s[i]=='{' || s[i]=='[')st.push(s[i]);
            else if(!st.empty() && st.top()=='(' && s[i]==')'){
                st.pop();
            }else if(!st.empty() && st.top()=='{' && s[i]=='}'){
                st.pop();
            }else if(!st.empty() && st.top()=='[' && s[i]==']'){
                st.pop();
            }else{
                return false;
            }
        }
        if(st.size())return false;
        
        return true;
    }
};
```

## Problem 4: Valid Parenthesis String

### 🔹 Topic
- Stack
- Greedy
- Strings

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Used two stacks to store the indices of `'('` and `'*'` characters separately.
- Traversed the string from left to right:
  - Stored the index of every `'('` in the first stack.
  - Stored the index of every `'*'` in the second stack.
  - For every `')'`, first tried to match it with the nearest unmatched `'('`.
  - If no `'('` was available, used a `'*'` as `'('`.
  - If neither was available, returned `false`.
- After processing the string, some `'('` might still remain unmatched.
- Matched each remaining `'('` with a `'*'` that appeared **after** it in the string.
- If no such `'*'` existed or its index was before `'('`, returned `false`.
- If all unmatched `'('` were successfully matched, returned `true`.

### 🔹 Time Complexity
- O(n)
  - Each character is pushed to or popped from a stack at most once.

### 🔹 Space Complexity
- O(n)
  - Two stacks are used to store the indices of `'('` and `'*'`.

### 🔹 Concepts Used
- Stack
- Greedy Matching
- Index Tracking
- Parentheses Validation
- String Traversal

### Solution
```cpp
class Solution {
public:
    bool checkValidString(string s) {
         int n=s.size();
         stack<int>st1;
         stack<int>st2;
         for(int i=0;i<n;i++){
            if(s[i]=='(')st1.push(i);
            else if(s[i]=='*')st2.push(i);
            else if(s[i]==')'){
               if(!st1.empty())st1.pop();
               else if(!st2.empty())st2.pop();
               else return false;
            }
         }
         while(!st1.empty()){
            if(st2.empty())return false;
            else if(st1.top() < st2.top()){
                st1.pop();
                st2.pop();
            }else{
                return false;
            }
         }

         return true;
    }
};
```

