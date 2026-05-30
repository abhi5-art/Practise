##  Daily Progress Overview - 29/05/2026

Today's preparation :
- Data Structures & Algorithms (Arrays)
- Aptitude Practice (Work - Pipes and tanks) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1:  Remove Duplicates from Sorted Array

- **Platform:** : Leetcode
- **Topic:** Array
- **Difficulty:** Medium
- **Concepts Used:**
  - Array
  - Two Pointer
  - Array Traversal

### Approach
- Used slow and fast pointer (sliding window) to track the all duplicates of every current element.
- window expands till the next distinct element appears, then appearing new element placed to its correct position by swapping.
- Traversed Array using 2 pointer technique and removed duplicates without affecting relative order of elements.

### Time Complexity
- `O(n)` for Array traversal
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& arr) {
        int n=arr.size();
        int i=0,j=1,cnt=0;
        while(j<n){
            if(arr[j]==arr[i]){
                j++;
            }else{
                i++;
                swap(arr[i],arr[j]);
                cnt++;
                j++;
            }
        }
        return cnt+1;
    }
};
```

## Problem 2: Max Consecutive Ones

- **Platform:** : Leetcode
- **Topic:** Array
- **Difficulty:** Easy
- **Concepts Used:**
  - Array Traversal

### Approach
- since array is binary , element can be 0 or 1 only. we can track no of contiguos 1s using single counter variable and make it 0 whenever 0 comes in array.
- To count maximum consecutive , we can compare counter variable with maximum(ans variable) for every increment of counter variable.
- At the end of traversal, maximum(ans variable) represents max consecutive 1s in array.

### Time Complexity
- `O(n)` for Array traversal 
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& arr) {
        int n=arr.size();
        int cnt=0,ans=0;
        for(int i=0;i<n;i++){
            if(arr[i]==0){
                cnt=0;
            }else{
                cnt++;
                ans=max(ans,cnt);
            }
        }
        return ans;
    }
};
```