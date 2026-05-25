##  Daily Progress Overview - 25/05/2026

Today's preparation :
- Data Structures & Algorithms (Monotonic Stack Problems)
- Aptitude Practice (Ratio and Proportion) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1: Next Greater Element I

- **Platform:** :contentReference[oaicite:0]{index=0}
- **Topic:** Monotonic Stack
- **Difficulty:** Easy
- **Concepts Used:**
  - Stack
  - Next Greater Element
  - Array Traversal

### Approach
- Used a monotonic decreasing stack to precompute next greater elements for `arr2`.
- Stored answers in a helper array.
- Traversed `arr1` and mapped corresponding answers from `arr2`.

### Time Complexity
- `O(n1 * n2)` for mapping + stack preprocessing

### Solution
```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& arr1, vector<int>& arr2) {
        int n1=arr1.size(),n2=arr2.size();
        vector<int>ans(n1);

        vector<int>great(n2,-1);
        stack<int>st;

        for(int i=0;i<n2;i++){
            while(!st.empty() && arr2[st.top()] < arr2[i]){
                great[st.top()]=arr2[i];
                st.pop();
            }
            st.push(i);
        }

        for(int i=0;i<n1;i++){
            for(int j=0;j<n2;j++){
                if(arr1[i]==arr2[j]){
                    ans[i]=great[j];
                    break;
                }
            }
        }

        return ans;
    }
};
```

## Problem 2: Next Greater Element II

- **Platform:** :contentReference[oaicite:0]{index=0}
- **Topic:** Monotonic Stack
- **Difficulty:** Medium
- **Concepts Used:**
  - Stack
  - Next Greater Element
  - Array Traversal

### Approach
- Since the array is circular, traversed the array twice (`2*n`) to simulate circular traversal.
- Used modulo operator `% n` to access elements in circular manner.
- Maintained a monotonic decreasing stack storing indices.
- Whenever current element became greater than stack top element, updated its next greater element.
- Stored answers in temporary array and copied first `n` answers to final result.

### Time Complexity
- `O(n)` for mapping + stack preprocessing

### Solution
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& arr) {
        int n=arr.size();
        stack<int>st;
        vector<int>ans(n);
        vector<int>temp(2*n,-1);

        for(int i=0;i<2*n;i++){
            while(!st.empty() && arr[st.top() % n] < arr[i%n]){
                temp[st.top()]=arr[i%n];
                st.pop();
            }
            st.push(i);
        }
        
        for(int i=0;i<n;i++)ans[i]=temp[i];
        return ans;
    }
};
```