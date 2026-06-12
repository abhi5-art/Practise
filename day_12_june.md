##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : 2D-Arrays, Binary Search
---

# DSA Problems Solved 

## Problem 1:  Find Peak Element

### 🔹 Topic
- Binary Search
- Arrays

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Handled the special case where the array contains only one element by directly returning its index.
- Applied binary search on the entire array.
- For each middle index:
  - If `mid` was the first element, checked whether it was greater than its next element.
  - If `mid` was the last element, checked whether it was greater than its previous element.
  - Otherwise, if the current element was greater than both its adjacent elements, identified it as a peak and returned its index.
- If the current element was greater than its left neighbor, moved to the right half since a peak must exist in that direction.
- Otherwise, moved to the left half where a peak was guaranteed to exist.
- Continued the process until a peak element was found.

### 🔹 Time Complexity
- O(log n)

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Binary Search
- Peak Property
- Search Space Reduction

### Solution
```cpp
class Solution {
public:
    int findPeakElement(vector<int>& arr) {
        int n=arr.size();
        int s=0,e=n-1,mid,ans;
        if(n==1)return 0;
        while(s<=e){
            mid = e+ (s-e)/2;
            if(mid==0){
                if(arr[mid]>arr[mid+1]){
                    ans=mid;
                    break;
                }else{
                    s=mid+1;
                }
            }else if(mid==n-1){
                if(arr[mid]>arr[mid-1]){
                    ans=mid;
                    break;
                }else{
                    e=mid-1;
                }
            }else if(arr[mid] > arr[mid-1] && arr[mid]>arr[mid+1]){
                ans=mid;
                break;
            }else if(arr[mid]>arr[mid-1]){
                s=mid+1;
            }else{
                e=mid-1;
            }
        }
        return ans;
    }
};
```