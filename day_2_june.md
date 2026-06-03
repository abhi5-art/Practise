##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms (Arrays)
- Aptitude Practice (Ratio and proportion) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1: Binary Search

- **Platform:** : Leetcode
- **Topic:** Binary search 
- **Difficulty:** Easy
- **Concepts Used:**
  - Array searching

### Time Complexity
- `O(logN)` for searching
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int search(vector<int>& arr, int x) {
        int s=0,e=arr.size()-1;
        while(s<=e){
            int mid= s+(e-s)/2;
            if(arr[mid]==x){
                return mid;
            }else if(arr[mid]>x){
                e=mid-1;
            }else{
                s=mid+1;
            }
        }
        return -1;
    }
};
```

## Problem 2: Find First and Last Position of Element in Sorted Array

- **Platform:** : Leetcode
- **Topic:** Binary Search
- **Difficulty:** Medium
- **Concepts Used:**
  - Array Searching

### Time Complexity
- `O(logN)` for searching 
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& arr, int x) {
        vector<int>ans;
        int n=arr.size();
        int s=0,e=n-1,mid,left=-1,right=-1;
        while(s<=e){
            mid = s+ (e-s)/2;
            if(arr[mid]==x){
                left=mid;
                e=mid-1;
            }else if(arr[mid]<x){
                s=mid+1;
            }else{
                e=mid-1;
            }
        }
        s=0;
        e=n-1;
        while(s<=e){
            mid = s+ (e-s)/2;
            if(arr[mid]==x){
                right=mid;
                s=mid+1;
            }else if(arr[mid]<x){
                s=mid+1;
            }else{
                e=mid-1;
            }
        }
        ans.push_back(left);
        ans.push_back(right);
        return ans;
    }
};
```