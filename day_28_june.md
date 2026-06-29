##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Sliding Window
---

# DSA Problems Solved 

## Problem 1: Count Number of Nice Subarrays

### 🔹 Topic
- Sliding Window
- Two Pointers

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that the number of subarrays containing exactly `k` odd numbers can be computed as:
  - `Exactly K Odds = At Most K Odds − At Most (K−1) Odds`.
- Implemented a helper function to count subarrays containing at most `k` odd numbers using the sliding window technique.
- Maintained a counter to track the number of odd elements in the current window.
- Expanded the window by moving the right pointer.
- Whenever the count of odd numbers exceeded `k`, shrank the window from the left until the condition became valid again.
- For every valid window, added `(j - i + 1)` to the answer since all subarrays ending at the current position were valid.
- Computed the final answer by subtracting the count of subarrays with at most `k−1` odd numbers from the count of subarrays with at most `k` odd numbers.

### 🔹 Time Complexity
- O(n)
  - Each element enters and leaves the sliding window at most once.

### 🔹 Space Complexity
- O(1)
  - Only a few variables are used to maintain the window.

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Variable Size Window
- At Most K Technique
- Inclusion-Exclusion Principle
- Counting Subarrays

### Solution
```cpp
class Solution {
    int atMost(vector<int>&arr, int k){
        int n=arr.size(),i=0,j=0,ans=0,cnt=0;
        while(j<n){
            if(arr[j]%2)cnt++;
            while(i<=j && cnt>k){
                if(arr[i]%2)cnt--;
                i++;
            }
            if(j<n && cnt<=k)ans+=(j-i+1);

            j++;
        }
        return ans;
    }
public:
    int numberOfSubarrays(vector<int>& arr, int k) {
         return atMost(arr,k) - atMost(arr,k-1);
    }
};
```


## Problem 2: Binary Subarrays With Sum

### 🔹 Topic
- Sliding Window
- Two Pointers
- Prefix Sum Observation

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that the number of subarrays having exactly `k` ones can be computed using:
  - `Exactly K Ones = At Most K Ones − At Most (K−1) Ones`.
- Implemented a helper function to count subarrays containing at most `k` ones using the sliding window technique.
- Maintained a counter to track the number of `1`s in the current window.
- Expanded the window by moving the right pointer.
- Whenever the count of `1`s exceeded `k`, shrank the window from the left until the condition became valid again.
- For every valid window, added `(j - i + 1)` to the answer since all subarrays ending at the current index satisfied the condition.
- Computed the final answer by subtracting the count of subarrays with at most `k−1` ones from the count of subarrays with at most `k` ones.

### 🔹 Time Complexity
- O(n)
  - Each element enters and leaves the sliding window at most once.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Variable Size Window
- At Most K Technique
- Inclusion-Exclusion Principle
- Counting Subarrays

### Solution
```cpp
class Solution {
    int atMost(vector<int>&arr,int k){
        int n=arr.size(),i=0,j=0,cnt=0,ans=0;
        while(j<n){
            if(arr[j]==1)cnt++;
            while(i<=j && cnt>k){
                if(arr[i]==1)cnt--;
                i++;
            }
            if(j<n && cnt<=k)ans+=j-i+1;

            j++;
        }
        return ans;
    }
public:
    int numSubarraysWithSum(vector<int>& arr, int k) {
        return atMost(arr,k)-atMost(arr,k-1);
    }
};
```
