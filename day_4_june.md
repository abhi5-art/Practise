##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Binary search
- Core Subject Preparation : Database Management System 

---

# DSA Problems Solved 

## Problem 1: Find out how many times the array is rotated

- **Platform:** : Striver
- **Topic:** Binary search 
- **Difficulty:** Medium
- **Concepts Used:**
  - Binary search 
  - Rotated Array

### 🔹 Approach
- Used binary search to locate the minimum element in the rotated sorted array.
- Compared the middle element with the first element of the array to identify whether it belonged to the left sorted portion or the right rotated portion.
- If `arr[mid] >= arr[0]`, the minimum element must lie further to the right, so moved the search space to the right half.
- Otherwise, stored the current index as a potential answer and continued searching in the left half for an earlier occurrence of the minimum element.
- The final index of the minimum element represents the number of rotations performed on the array.

### Time Complexity
- `O(logN)` for searching
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int findKRotation(vector<int> &arr)  {
        int n=arr.size(),mini=0;
        int start=0,end=n-1;

        while(start <= end){
            int mid = start + (end-start)/2;

            if(arr[mid] >= arr[0]){
                start = mid+1;
            }else{
                mini=mid;
                end=mid-1;
            }
        }

        return mini;
    }
};
```

## Problem 2: Single Element in a Sorted Array

- **Platform:** : Leetcode
- **Topic:** Binary Search
- **Difficulty:** Medium
- **Concepts Used:**
  - Binary search 
  - Sorted array

### 🔹 Approach
- Used binary search instead of the linear XOR approach since the array is sorted.
- Observed that before the single element, pairs start at even indices and end at odd indices.
- After the single element, this pattern gets disrupted.
- For each middle index:
  - If the pairing pattern was correct (`even → next` or `odd → previous`), the single element must lie on the right side.
  - If the pairing pattern was broken (`odd → next` or `even → previous`), the single element must lie on the left side.
- If the current element did not match either adjacent element, it was identified as the single non-duplicate element.

### Time Complexity
- `O(logN)` for searching 
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int singleNonDuplicate(vector<int>& arr) {
        int n=arr.size(),ans=-1;
        /// This can be solved using linear approach of xor , but array is sorted so can be solved using binary search approach which is optimal for this problem.
        int start=0,end=n-1;
        while(start <= end){
            int mid = start + (end-start)/2;

            if((mid < n-1 && mid%2==0 && arr[mid]==arr[mid+1]) || (mid > 0 && mid%2==1 && arr[mid]==arr[mid-1])){
                 start = mid+1;
            }else if((mid < n-1 && mid%2==1 && arr[mid]==arr[mid+1]) || (mid > 0 && mid%2==0 && arr[mid]==arr[mid-1])){
                 end = mid-1;
            }else{
                ans = arr[mid];
                break;
            }
        }

        return ans;
    }
};
```