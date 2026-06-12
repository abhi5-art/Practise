##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : 2D-Arrays, Binary Search
---

# DSA Problems Solved 

## Problem 1:  Find row with maximum 1's

### 🔹 Topic
- Binary Search
- 2D Arrays
- Matrix

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Traversed each row of the matrix individually.
- For every row, used binary search to find the index of the first occurrence of `1`.
- Initialized the index as `n`, assuming that the row contained no `1`s.
- Whenever a `1` was found at the middle index, stored that index as a potential answer and continued searching in the left half to find the first occurrence.
- Calculated the number of `1`s in the current row as `n - index`.
- Compared this count with the maximum number of `1`s found so far.
- Updated the answer with the current row index whenever a row with more `1`s was found.
- Returned the index of the row having the maximum number of `1`s. If no `1`s were present in the matrix, returned `-1`.

### 🔹 Time Complexity
- O(m × log n)
  - Binary search is performed for each of the `m` rows.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Binary Search
- First Occurrence of an Element
- Matrix Traversal

### Solution
```cpp
class Solution {
  public:   
  int rowWithMax1s(vector < vector < int >> & mat) {
      int ans=-1,m=mat.size(),n=mat[0].size(),maxi=0;
      
      int start,end,mid;
      for(int i=0;i<m;i++){
        start=0,end=n-1;
        int index=n;
        while(start <= end){
            mid = start + (end-start)/2;
            if(mat[i][mid] == 1){
                index = mid;
                end = mid-1;
            }else{
                start = mid+1;
            }
        }
        if((n-index) > maxi){
            maxi=(n-index);
            ans=i;
        }
      }

      return ans;
  }
};
```

## Problem 2: Search a 2D Matrix

### 🔹 Topic
- Binary Search
- 2D Arrays
- Matrix

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that the given matrix follows the property of a globally sorted array.
- Considered the entire matrix as a virtual 1D array of size `m × n`.
- Applied binary search on the index range from `0` to `m*n - 1`.
- Converted the middle index of the virtual array back to matrix coordinates using:
  - `row = mid / n`
  - `col = mid % n`
- Compared the element at `(row, col)` with the target:
  - If equal, returned `true`.
  - If greater, searched in the left half.
  - If smaller, searched in the right half.
- Continued until the target was found or the search space became empty.

### 🔹 Time Complexity
- O(log (m × n))

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- Binary Search
- Index Mapping
- Virtual 1D Representation of a Matrix

### Solution
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& mat, int target) {
        int m=mat.size(),n=mat[0].size();
        int start=0,end=m*n - 1;

        while(start <= end){
            int mid = start + (end - start)/2;
            int i= mid/n;
            int j=mid%n;
            if(mat[i][j] == target){
                 return 1;
            }else if(mat[i][j] > target){
                end=mid-1;
            }else{
                start=mid+1;
            }
        }

        return 0;
    }
};
```