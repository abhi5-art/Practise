##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Arrays,subarrays
---

# DSA Problems Solved 

## Problem 1: Find All Lonely Numbers in the Array

### 🔹 Topic
- Hashing
- Arrays
- Frequency Counting

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Used a hash map to store the frequency of every element in the array.
- Traversed the array and checked each element against the lonely number conditions:
  - The element must appear exactly once in the array.
  - The element immediately smaller (`x - 1`) should not exist in the array.
  - The element immediately larger (`x + 1`) should not exist in the array.
- If all conditions were satisfied, added the element to the answer vector.
- Returned all such lonely numbers.

### 🔹 Time Complexity
- O(n)
  - One traversal to build the frequency map and another traversal to identify lonely numbers.

### 🔹 Space Complexity
- O(n)
  - Additional space is used for the frequency map.

### 🔹 Concepts Used
- Hash Map (`unordered_map`)
- Array Traversal

### Solution
```cpp
class Solution {
public:
    vector<int> findLonely(vector<int>& arr) {
        int n=arr.size();
        unordered_map<int,int>m;
        vector<int>ans;
        
        for(auto x:arr)m[x]++;

        for(auto x:arr){
            if(m[x]==1 && m.find(x-1)==m.end() && m.find(x+1)==m.end()){
                ans.push_back(x);
            }
        }
        return ans;
    }
};
```

## Problem 2: Subarrays with K Different Integers

### 🔹 Topic
- Sliding Window
- Two Pointers
- Hashing

### 🔹 Difficulty
- Hard

### 🔹 Approach
- Used the observation:
  - `Exactly K Distinct = At Most K Distinct − At Most (K−1) Distinct`.
- Implemented a helper function to count subarrays containing at most `k` distinct integers.
- Maintained a sliding window using two pointers and a frequency map.
- Expanded the window by moving the right pointer and updating the frequency of the current element.
- Whenever the number of distinct elements exceeded `k`, shrank the window from the left until the condition became valid again.
- For every valid window, added `(j - i + 1)` to the answer since all subarrays ending at the current index and starting within the window were valid.
- Computed the final answer by subtracting the count of subarrays with at most `k−1` distinct integers from the count of subarrays with at most `k` distinct integers.

### 🔹 Time Complexity
- O(n)
  - Each element is added to and removed from the sliding window at most once.

### 🔹 Space Complexity
- O(k)
  - The frequency map stores at most `k + 1` distinct integers.

### 🔹 Concepts Used
- Sliding Window
- Two Pointers
- Hash Map (`unordered_map`)
- Frequency Counting
- Inclusion-Exclusion Principle
- Counting Subarrays


### Solution
```cpp
class Solution {
    int solve(vector<int>&arr, int k){
       unordered_map<int,int>m;
       int n=arr.size(),i=0,j=0,ans=0;
       while(j<n){
           m[arr[j]]++;
           while(i<=j && m.size() > k){
               if(m[arr[i]] == 1)m.erase(arr[i]);
               else m[arr[i]]--;
               i++;
           }
           ans = ans + (j-i+1);
           j++;
       }
       return ans;
    }
public:
    int subarraysWithKDistinct(vector<int>& arr, int k) {
       int a=solve(arr,k);
       int b=solve(arr,k-1); 
       return a-b;
    }
};
```