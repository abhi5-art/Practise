##  Daily Progress Overview - 26/05/2026

Today's preparation :
- Data Structures & Algorithms (Subarrays, String)
- Aptitude Practice (Percentage) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1: Password Strength

- **Platform:** : Leetcode
- **Topic:** String
- **Difficulty:** Easy
- **Concepts Used:**
  - String
  - Hashmap
  - String Traversal

### Approach
- Used hashmap to track current character is distinct or not while traversing in string.
- updated frequency of characters in hashmap.
- Traversed string and for each character strength is stored according to char type.

### Time Complexity
- `O(n)` for string traversal
### Space Complexity
- `O(n)` for hashmap (storing freauency)

### Solution
```cpp
class Solution {
public:
    int passwordStrength(string str) {
        int ans=0,n=str.size();
        unordered_map<char,int>m;
        for(int i=0;i<n;i++){
            m[str[i]]++;

            if(m[str[i]] == 1){
                if(islower(str[i]))ans++;
                else if(isupper(str[i]))ans+=2;
                else if(isdigit(str[i]))ans+=3;
                else{
                    ans+=5;
                }
            }
        }
        return ans;
    }
};
```

## Problem 2: Sum of Subarray Minimums

- **Platform:** : Leetcode
- **Topic:** Subarray-Monotonic stack
- **Difficulty:** Medium
- **Concepts Used:**
  - Stack
  - Next smaller Element
  - Array Traversal

### Approach
- we can compute the no of subarrays for which every current element in array is minimum.
- For that , next smaller and previous smaller element index must be known at every index.so that no of possible subarrays for every index can be computed.
- Maintained a monotonic increasing stack storing indices.
- Whenever current element became smaller than stack top element, updated its next/previous smaller element's index.
- Stored next and previous smaller element's indexes in separate arrays for efficient handling.
- Traversed array and calculated total sum with the help of precomputed smaller/previous element indexes.

### Time Complexity
- `O(n)` for mapping + stack preprocessing
### Space Complexity
- `O(n)` for storing indexes of next and previous smaller element

### Solution
```cpp
class Solution {
public:
    void next(vector<int>&arr, vector<int>&next_small, int n){
       stack<int>st;
       for(int i=0;i<n;i++){
         while(!st.empty() && arr[st.top()] >= arr[i]){
            next_small[st.top()]=i;
            st.pop();
         }
         st.push(i);
       }
    }
    void prev(vector<int>&arr, vector<int>&prev_small, int n){
       stack<int>st;
       for(int i=n-1;i>=0;i--){
        while(!st.empty() && arr[st.top()] > arr[i]){
            prev_small[st.top()]=i;
            st.pop();
         }
         st.push(i);
       }
    }
    int sumSubarrayMins(vector<int>& arr) {
       int n=arr.size();
       long long ans=0,con = 1e9 + 7;
       
       vector<int>next_small(n,n);
       vector<int>prev_small(n,-1);

       next(arr,next_small,n);
       prev(arr,prev_small,n);

       for(int i=0;i<n;i++){
           int a = next_small[i] - i;
           int b = i - prev_small[i];
           long long temp = (a*b) % con;
           ans = ans + (temp*arr[i] % con);
       }

       return ans % con;
    }
};
```