##  Daily Progress Overview - 28/05/2026

Today's preparation :
- Data Structures & Algorithms (Substrings, Subarrays)
- Aptitude Practice (Mixtures, Average) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1:  Number of Substrings With Only 1s

- **Platform:** : Leetcode
- **Topic:** String
- **Difficulty:** Medium
- **Concepts Used:**
  - String
  - Sliding Window
  - String Traversal

### Approach
- Used slow and fast pointer (sliding window) to track the contigious substring of 1s.
- window expands to get maximum possible substring of 1s,then no of posssible substrings in it computed and window gets compressed for further computation.
- Traversed string and computed total no of possible substrings with only 1s.

### Time Complexity
- `O(n)` for string traversal
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int numSub(string s) {
        int n=s.size();
        long long int con = 1e9 + 7,ans=0,t;
        int i=0,j=0;
        while(j<n){
            while(i<=j && s[j]=='0'){
                t=j-i;
                t = t*(t+1)/2;
                t = t % con;
                ans+=t;
                j++;
                i=j;
            }
            if(j<n && s[j]=='1')j++;
        }
        t=j-i;
        t = t*(t+1)/2;
        t = t % con;
        ans+=t;

        return ans % con;
    }
};
```

## Problem 2:  Minimum Size Subarray Sum

- **Platform:** : Leetcode
- **Topic:** Subarray-sliding window
- **Difficulty:** Medium
- **Concepts Used:**
  - Sliding Window (2 pointer)
  - Array Traversal

### Approach
- we can use sliding window technique in which window can be expanded until the sum gets greater than or equal to target. Then we can compress window until condition remain satisfied.
- While window compression , minimal length of subarray computed .

### Time Complexity
- `O(n)` for Array traversal using 2 pointers
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int minSubArrayLen(int x, vector<int>& arr) {
        int n=arr.size(),ans=INT_MAX,i=0,j=0,sum=0;

        while(j<n){
            sum+=arr[j];
            while(i<=j && sum >= x){
                ans=min(ans,j-i+1);
                sum-=arr[i];
                i++;
            }
            if(j<n && sum < x)j++;
        }
        if(ans == INT_MAX)return 0;
        return ans;
    }
};
```