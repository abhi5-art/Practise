##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Sliding Window
---

# DSA Problems Solved 

## Problem 1: Number of Substrings Containing All Three Characters

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Used a sliding window with two pointers to maintain the current substring.
- Expanded the window by moving the right pointer and updating the frequency of each character using a hash map.
- Whenever the current window contained at least one occurrence of `'a'`, `'b'`, and `'c'`, it formed a valid substring.
- Since every extension of this valid window to the right would also remain valid, added `(n - j)` to the answer.
- Shrank the window from the left by decreasing character frequencies until the window was no longer valid.
- Repeated the process until the entire string was traversed.

### 🔹 Time Complexity
- O(n)
  - Each character enters and leaves the sliding window at most once.

### 🔹 Space Complexity
- O(1)
  - The frequency map stores at most three characters (`a`, `b`, and `c`).

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Frequency Counting
- Counting Valid Substrings


### Solution
```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
       unordered_map<char,int>m;
       int n=s.size(),i=0,j=0,ans=0;
       while(j<n){
          m[s[j]]++;
          while(i<=j && m['a']>=1 && m['b']>=1 && m['c']>=1){
             ans+=(n-j);
             if(m[s[i]]==1)m.erase(s[i]);
             else m[s[i]]--;
             i++;
          }
          j++;
       } 
       return ans;
    }
};
```


## Problem 2: Fruit Into Baskets

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that the problem requires finding the longest contiguous subarray containing at most two distinct fruit types.
- Used a sliding window with two pointers to maintain the current range of trees.
- Maintained a hash map to store the frequency of each fruit type present in the current window.
- Expanded the window by moving the right pointer and updating the fruit frequency.
- Whenever the number of distinct fruit types exceeded two, shrank the window from the left by decreasing frequencies and removing fruit types whose count became zero.
- After each valid window, updated the maximum number of fruits that could be collected.
- Returned the maximum window size obtained during the traversal.

### 🔹 Time Complexity
- O(n)
  - Each tree is added to and removed from the sliding window at most once.

### 🔹 Space Complexity
- O(1)
  - The hash map stores at most three fruit types during processing (effectively constant space).

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Variable Size Window
- Longest Subarray with At Most K Distinct Elements

### Solution
```cpp
class Solution{
  public:
    int totalFruits(vector<int>& arr){
        int n=arr.size();
        unordered_map<int,int>m;
        int i=0,j=0,ans=0;
        while(j<n){
            m[arr[j]]++;
            while(i<=j && m.size()>2){
                if(m[arr[i]] ==1)m.erase(arr[i]);
                else m[arr[i]]--;
                i++;
            }
            ans=max(ans,j-i+1);
            j++;
        }
        return ans;
    }
};
```
