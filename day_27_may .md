##  Daily Progress Overview - 27/05/2026

Today's preparation :
- Data Structures & Algorithms (Substrings, Subarrays)
- Aptitude Practice (Profit Loss) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1:  Count Number of Homogenous Substrings

- **Platform:** : Leetcode
- **Topic:** String
- **Difficulty:** Medium
- **Concepts Used:**
  - String
  - Sliding Window
  - String Traversal

### Approach
- Used slow and fast pointer (sliding window) to track the current homogeneous substring.
- window expands to get maximum possible substring,then no of posssible substrings in it computed and window gets compressed for further computation.
- Traversed string and computed total no of possible homogenous substrings.

### Time Complexity
- `O(n)` for string traversal
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int countHomogenous(string s) {
        int n=s.size();
        long long int ans=0, con = 1e9 + 7;

        int i=0,j=0;
        long long int t;
        char el=s[0];
        while(j<n){
            if(i<=j && s[j] != el){
                el=s[j];
                t=(j-i);
                t = t*(t+1)/2;
                t = t % con;
                ans+=t;
                i=j;
            }
            j++;
        } 
        t = j-i;
        t = t*(t+1)/2;
        t = t% con;
        ans+=t;
 
        return ans % con;
    }
};
```

## Problem 2: Sum of Subarray Ranges

- **Platform:** : Leetcode
- **Topic:** Subarray-Monotonic stack
- **Difficulty:** Medium
- **Concepts Used:**
  - Stack
  - Next smaller Element
  - Next greater Element
  - Array Traversal

### Approach
- we can compute the no of subarrays for which every current element in array is minimum and maximum.
- For Minimum element in subarray, next smaller and previous smaller element index must be known at every index.so that no of possible subarrays for every index can be computed.similarly for Maximum element in subarray, next greater and previous greater element index must be known at every index.
- Maintained a monotonic increasing and decreasing stack storing indices.
- Stored next and previous smaller/greater element's indexes in separate arrays for efficient handling.
- Traversed array and calculated total sum with the help of precomputed smaller/previous element indexes.

### Time Complexity
- `O(n)` for mapping + stack preprocessing
### Space Complexity
- `O(n)` for storing indexes of next/previous smaller and greater element

### Solution
```cpp
class Solution {
    void next_great(vector<int>&ans,vector<int>&arr){
        stack<int>st;
        for(int i=0;i<arr.size();i++){
            while(!st.empty() && arr[st.top()] <= arr[i]){
                ans[st.top()]=i;
                st.pop();
            }
            st.push(i);
        }
    }
    void prev_great(vector<int>&ans,vector<int>&arr){
        stack<int>st;
        for(int i=arr.size()-1;i>=0;i--){
            while(!st.empty() && arr[st.top()] < arr[i]){
                ans[st.top()]=i;
                st.pop();
            }
            st.push(i);
        }
    }
    void next_small(vector<int>&ans,vector<int>&arr){
        stack<int>st;
        for(int i=0;i<arr.size();i++){
            while(!st.empty() && arr[st.top()] >= arr[i]){
                ans[st.top()]=i;
                st.pop();
            }
            st.push(i);
        }
    }
    void prev_small(vector<int>&ans,vector<int>&arr){
        stack<int>st;
        for(int i=arr.size()-1;i>=0;i--){
            while(!st.empty() && arr[st.top()] > arr[i]){
                ans[st.top()]=i;
                st.pop();
            }
            st.push(i);
        }
    }
public:
    long long subArrayRanges(vector<int>& arr) {
        int n=arr.size();
        long long int maxi=0,mini=0;
        
        vector<int>rg(n,n);
        vector<int>lg(n,-1);
        vector<int>rsm(n,n);
        vector<int>lsm(n,-1);
        next_great(rg,arr);
        prev_great(lg,arr);
        next_small(rsm,arr);
        prev_small(lsm,arr);
        
        for(int i=0;i<n;i++){
            long long k=(rg[i]-i)*(i-lg[i]);
           maxi += (k*arr[i]);
             
             k=(rsm[i]-i)*(i-lsm[i]);
           mini += (k*arr[i]);
        }

        return maxi-mini;
    }
};
```