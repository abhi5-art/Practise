##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms (Arrays)
- Core Subject Revision : Operating System (fundamental topics)

---

# DSA Problems Solved 

## Problem 1:  Digit Frequency Score

- **Platform:** : Leetcode
- **Topic:** Number 
- **Difficulty:** Easy
- **Concepts Used:**
  - Hashmap
  - Number theory

### Approach
- Score of number n depend on sum of multiplication of every distinct digit and its frequency.
- used hashmap to track every digit and its frequency in number n;
- Traversed digits in n using modulo operator to store d and freq(d) in map.
- Traversed hashmap to compute final answer value.

### Time Complexity
- `O(logN)` for digits traversal
### Space Complexity
- `O(logN)` for storing all digits in N

### Solution
```cpp
class Solution {
public:
    int digitFrequencyScore(int n) {
        unordered_map<int,int>m;
        int t=n;
        while(t > 0){
            m[t%10]++;
            t=t/10;
        }
        int ans=0;
        for(auto x:m){
            ans+=x.first*x.second;
        }
        return ans;
    }
};
```

## Problem 2: Max Consecutive Ones

- **Platform:** : Leetcode
- **Topic:** Array
- **Difficulty:** Medium
- **Concepts Used:**
  - Sliding Window technique
  - Array Traversal

### Approach
- since array is binary , Maximum consecutive 1s with atmost k flips of 0s can be considered as longest subarray with atmost k 0s.
- so this problem becomes sliding window type , where window can be exanded till no of 0s are less than or equal to k, and window compressed if (cnt > k).
- Used sliding window technique to compute the answer value using slow and fast pointer.

### Time Complexity
- `O(N)` for Array traversal 
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int longestOnes(vector<int>& arr, int k) {
        int n=arr.size(),ans=0,i=0,j=0,cnt=0;

        while(j<n){
            if(arr[j]==0)cnt++;
            while(i<=j && cnt > k){
                if(arr[i]==0)cnt--;
                i++;
            }
            if(j<n && cnt <= k){
                ans=max(ans,j-i+1);
                j++;
            }
        }
        return ans;
    }
};
```