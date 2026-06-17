##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : sliding window
---

# DSA Problems Solved 

## Problem 1: Longest Substring Without Repeating Characters

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Used a sliding window with two pointers (`i` and `j`) to maintain a substring containing unique characters.
- Expanded the window by moving the right pointer and updating the frequency of the current character in a hash map.
- If a character appeared more than once, shrank the window from the left until all characters in the current window became unique again.
- After every valid window, updated the maximum substring length.
- Continued the process until the entire string was traversed.

### 🔹 Time Complexity
- O(n)
  - Each character is added to and removed from the window at most once.

### 🔹 Space Complexity
- O(min(n, charset))
  - The hash map stores frequencies of characters present in the current window.

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Frequency Counting
- Variable Size Window


### Solution
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n=s.size(),i=0,j=0,ans=0;
        unordered_map<char,int>m;
        while(j<n){
            m[s[j]]++;
            while(i<=j && m[s[j]]> 1){
                if(m[s[i]]==1)m.erase(s[i]);
                else m[s[i]]--;
                i++;
            }
            ans=max(ans,j-i+1);
            j++;
        }

        return ans;
    }
};
```

## Problem 2: Count Complete Subarrays in an Array

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- First determined the total number of distinct elements present in the entire array using a set.
- Let this count be `k`.
- Observed that a complete subarray must contain all `k` distinct elements.
- Used the formula:
  - `Exactly K Distinct = At Most K Distinct − At Most (K−1) Distinct`.
- Implemented a helper function to count subarrays having at most `k` distinct elements using a sliding window.
- Maintained a frequency map for elements inside the current window.
- Expanded the window by moving the right pointer and updating frequencies.
- Whenever the number of distinct elements exceeded `k`, shrank the window from the left until the condition became valid again.
- For every valid window, added `(j - i + 1)` to the answer since all subarrays ending at the current index were valid.
- Computed the final answer by subtracting subarrays with at most `k−1` distinct elements from subarrays with at most `k` distinct elements.

### 🔹 Time Complexity
- O(n)
  - The sliding window helper runs in linear time.
  - The initial set construction also takes O(n).

### 🔹 Space Complexity
- O(k)
  - Additional space is used for the frequency map and set storing distinct elements.

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Hash Set (`unordered_set`)
- Frequency Counting
- Inclusion-Exclusion Principle
- Counting Subarrays


### Solution
```cpp
class Solution {
    int atMostK(vector<int>&arr,int k){
        int n=arr.size(),i=0,j=0,ans=0;
        unordered_map<int,int>m;
        while(j<n){
            m[arr[j]]++;
            while(i<=j && m.size() > k){
                if(m[arr[i]] == 1)m.erase(arr[i]);
                else m[arr[i]]--;
                i++;
            }
            ans+=(j-i+1);
            j++;
        }
        return ans;
    }
public:
    int countCompleteSubarrays(vector<int>& arr) {
        unordered_set<int>st;
        for(auto x:arr)st.insert(x);
        int k=st.size();
        
        return atMostK(arr,k) - atMostK(arr,k-1);
    }
};
```