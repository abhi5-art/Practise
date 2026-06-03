##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms (Rotated Arrays)
- Aptitude Practice (Ratio and proportion) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1: Search in Rotated Sorted Array

- **Platform:** : Leetcode
- **Topic:** Binary search 
- **Difficulty:** medium
- **Concepts Used:**
  - Binary search 
  - Rotated Array

### 🔹 Approach
- Used binary search to find the target element efficiently.
- Compared the middle element with the first element of the array to identify whether `mid` lies in the left sorted part or the right sorted part.
- If both the target and `mid` belonged to the same sorted portion, performed normal binary search within that portion.
- Otherwise, discarded the current portion and moved to the other half where the target could exist.
- Repeated the process until the target was found or the search space became empty.

### Time Complexity
- `O(logN)` for searching
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int search(vector<int>& arr, int x) {
        int n=arr.size();
        int start=0,end=n-1;
        while(start<=end){
            int mid = start + (end-start)/2;
            if(arr[mid] >= arr[0]){
               if(x >= arr[0]){
                   if(arr[mid] == x)return mid;
                   else if(x < arr[mid])end=mid-1;
                   else start=mid+1;
               }else{
                start=mid+1;
               }
            }else{
               if(x < arr[0]){
                   if(arr[mid] == x)return mid;
                   else if(x < arr[mid])end=mid-1;
                   else start=mid+1;
               }else{
                 end=mid-1;
               }
            }
        }

        return -1;
    }
};
```

## Problem 2: Search in Rotated Sorted Array II

- **Platform:** : Leetcode
- **Topic:** Binary Search
- **Difficulty:** Medium
- **Concepts Used:**
  - Binary search 
  - Rotated Array

### 🔹 Approach
- Inserted all array elements into a set to remove duplicate values.
- Copied the unique elements from the set into a new vector.
- Applied binary search on the resulting array.
- Compared the middle element with the first element to determine whether `mid` belonged to the left sorted portion or the right sorted portion.
- If the target and middle element were in the same sorted portion, performed normal binary search.
- Otherwise, discarded the current portion and continued searching in the remaining half.
- Returned `true` if the target was found; otherwise returned `false`.

### Time Complexity
- `O(logN)` for searching 
### Space Complexity
- `O(N)` for storing distinct elements in array and stack

### Solution
```cpp
class Solution {
public:
    bool search(vector<int>& nums, int x) {
        int n=nums.size();
        set<int>st;
        vector<int>arr;
        for(auto x:nums)st.insert(x);
        for(auto x:st)arr.push_back(x);
        int s=0,e=arr.size()-1,mid;
        while(s<=e){
            mid = s+ (e-s)/2;
            if(arr[mid] >= arr[0]){
               //left sorted array
               if(x >= arr[0]){
                  if(arr[mid] == x){
                    return  1;
                  }else if(arr[mid]<x){
                    s=mid+1;
                  }else{
                    e=mid-1;
                  }
               }else{
                 s=mid+1;
               }
            }else{
                if(x < arr[0]){
                  if(arr[mid] == x){
                    return 1;
                  }else if(arr[mid]<x){
                    s=mid+1;
                  }else{
                    e=mid-1;
                  }
               }else{
                 e=mid-1;
               }
            }
        }

        return 0;
    }
};
```


## Problem 3: Find Minimum in Rotated Sorted Array
- **Platform:** : Leetcode
- **Topic:** Binary search 
- **Difficulty:** medium
- **Concepts Used:**
  - Binary search 
  - Rotated Array

### 🔹 Approach
- Initialized the answer with the first element of the array.
- Used binary search to determine whether the middle element belonged to the left sorted portion or the right rotated portion.
- If `arr[mid] >= arr[0]`, the minimum element must lie further to the right, so moved the search space to the right half.
- Otherwise, updated the answer with `arr[mid]` and continued searching in the left half to find a potentially smaller element.
- Repeated the process until the search space was exhausted.

### Time Complexity
- `O(logN)` for searching
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int findMin(vector<int>& arr) {
        int n=arr.size(),ans=arr[0];
        int start=0,end=n-1;
        while(start <= end){
            int mid = start + (end-start)/2;

            if(arr[mid] >= arr[0]){
                start = mid+1;
            }else{
                ans=arr[mid];
                end=mid-1;
            }
        }
        return ans;
    }
};
```