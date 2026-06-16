##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : sliding window (substrings)
---

# DSA Problems Solved 

## Problem 1: Count Substrings With K-Frequency Characters

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Used a sliding window with two pointers (`i` and `j`) to examine substrings efficiently.
- Expanded the window by moving the right pointer and updating the frequency of the current character using an unordered map.
- Whenever the frequency of the character at the right pointer became exactly `k`, all substrings starting from the current left pointer and ending at any position from `j` to `n-1` became valid.
- Added `(n - j)` to the answer since extending the current valid substring to the right would also satisfy the condition.
- Shrank the window from the left by updating frequencies and moving the left pointer until the frequency condition was no longer met.
- Continued this process until the right pointer reached the end of the string.

### 🔹 Time Complexity
- O(n)
  - Each character is added to and removed from the sliding window at most once.

### 🔹 Space Complexity
- O(1)
  - The frequency map stores counts for a limited set of characters (constant alphabet size).

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Frequency Counting
- Hash Map (`unordered_map`)
- Counting Valid Substrings

### Solution
```cpp
class Solution {
public:
    int numberOfSubstrings(string s, int k) {
        int n=s.size(),ans=0;
        unordered_map<char,int>m;
        int i=0,j=0;
        while(j<n){
            m[s[j]]++;
            while(i<=j && m[s[j]]==k){
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

## Problem 2: Count Number of Substrings

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Used the observation that:
  - `Exactly K Distinct = At Most K Distinct − At Most (K−1) Distinct`.
- Implemented a helper function to count substrings containing at most `k` distinct characters using the sliding window technique.
- Maintained a frequency map to track character occurrences within the current window.
- Expanded the window by moving the right pointer and adding the current character to the map.
- Whenever the number of distinct characters exceeded `k`, shrank the window from the left by decreasing frequencies and removing characters whose frequency became zero.
- For every valid window, added `(right - left + 1)` to the result since all substrings ending at the current right pointer and starting within the window were valid.
- Computed the final answer by subtracting the count of substrings with at most `k-1` distinct characters from the count of substrings with at most `k` distinct characters.

### 🔹 Time Complexity
- O(n)
  - The helper function runs in `O(n)` time.
  - Since it is called twice, the overall complexity remains `O(n)`.

### 🔹 Space Complexity
- O(k)
  - The frequency map stores at most `k + 1` distinct characters at any point.

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Frequency Counting
- Inclusion-Exclusion Principle
- Counting Subarrays/Substrings

### Solution
```cpp
class Solution {
    int atMostK(string s, int k) {
        int i=0,ans=0,j=0,n=s.size();
        unordered_map<char, int> m;

        while (j<n>) {
            m[s[j]]++;

            while (m.size() > k) {
                m[s[i]]--;
                if (m[s[i]] == 0) {
                    m.erase(s[i]);
                }
                i++;
            }

            ans += (j - i + 1);
            j++;
        }

        return ans;
    }

public:
    int countSubstrings(string s, int k) {
        return atMostK(s, k) - atMostK(s, k - 1);
    }
};
```