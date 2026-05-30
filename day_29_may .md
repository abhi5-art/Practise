##  Daily Progress Overview - 29/05/2026

Today's preparation :
- Data Structures & Algorithms (Arrays)
- Aptitude Practice (Time and Work) : Indiabix Platform

---

# DSA Problems Solved 

## Problem 1: Two Sum

- **Platform:** : Leetcode
- **Topic:** Array
- **Difficulty:** Easy
- **Concepts Used:**
  - Array
  - Hashmap
  - Array Traversal

### Approach
- Instead of finding pair of 2 sum directly , we can find whether (target-arr[i]) exists in array or not using hashmap.
- Used hashmap to track element and its index.
- Traversed Array and checked pair for every element using hashmap. when pair gets , loop breaks as we gets solution.
- This Approach is optimzed for this problem.

### Time Complexity
- `O(n)` for array traversal
### Space Complexity
- `O(n)` for hashmap 

### Solution
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& arr, int x) {
        vector<int>ans;
        int n=arr.size();
        unordered_map<int,int>m;

        for(int i=0;i<n;i++){
            if(m.find(x-arr[i]) != m.end()){
                ans.push_back(m[x-arr[i]]);
                ans.push_back(i);
                break;
            }
            m[arr[i]]=i;
        }
        return ans;
    }
};
```

## Problem 2:  Majority Element

- **Platform:** : Leetcode
- **Topic:** Array
- **Difficulty:** Easy
- **Concepts Used:**
  - Array Traversal

### Approach
- There are multiple approaches. simplest approach is track the frequencies of elements using hashmap. Then search in hashmap for the element with frequency greater than n/2. But it takes O(N) time complexity as well as space complexity.
-  Optimized Approach called as Morre's Voting Algorithm. It uses 1 element variable and 1 count variable .
-  Traverse array ,if cnt = 0 then choose arr[i] as element, else if arr[i] equals element then increment. else decrement it. final element variable represents majority element.

### Time Complexity
- `O(n)` for Array traversal
### Space Complexity
- `O(1)` for variables

### Solution
```cpp
class Solution {
public:
    int majorityElement(vector<int>& arr) {
        int n=arr.size(),cnt=0,element;
        for(int i=0;i<n;i++){
            if(cnt == 0){
                cnt=1;
                element=arr[i];
            }else if(arr[i] == element){
                cnt++;
            }else{
                cnt--;
            }
        }

        return element;
    }
};
```