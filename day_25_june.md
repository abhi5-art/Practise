##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Array,String
---

# DSA Problems Solved 

## Problem 1: Sort Characters By Frequency

### 🔹 Topic
- Strings
- Hashing
- Sorting

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Counted the frequency of each character using an unordered map.
- Stored each character along with its frequency as a pair `(frequency, character)` in a vector.
- Sorted the vector in descending order of frequency.
- Traversed the sorted vector and appended each character to the answer string according to its frequency.
- Returned the constructed string with characters arranged in decreasing order of frequency.

### 🔹 Time Complexity
- O(n + k log k)
  - `n` = length of the string.
  - `k` = number of distinct characters.
  - Frequency counting takes `O(n)` and sorting takes `O(k log k)`.

### 🔹 Space Complexity
- O(k)
  - Additional space is used for the hash map and vector of frequency pairs.

### 🔹 Concepts Used
- Hash Map (`unordered_map`)
- Frequency Counting
- Sorting
- Vector of Pairs
- Greedy Construction

### Solution
```cpp
class Solution {
public:
    string frequencySort(string s) {
        string ans="";
        unordered_map<char,int>m;
        for(auto x:s)m[x]++;

        vector<pair<int,char>>temp;
        pair<int,char>p;
        for(auto x:m){
           p.first=x.second;
           p.second=x.first;
           temp.push_back(p);
        }
        sort(temp.rbegin(), temp.rend());

        for(auto x:temp){
            for(int i=0;i<x.first;i++){
                ans+=x.second;
            }
        }

        return ans;
    }
};
```

## Problem 2: Sort Array by Increasing Frequency

### 🔹 Topic
- Arrays
- Hashing
- Sorting

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Counted the frequency of each element using an unordered map.
- Stored each element and its frequency as a pair `(frequency, value)` in a vector.
- Sorted the vector using a custom comparator:
  - Elements with smaller frequencies were placed first.
  - If two elements had the same frequency, the element with the larger value was placed first.
- Traversed the sorted vector and inserted each element into the answer array according to its frequency.
- Returned the final sorted array.

### 🔹 Time Complexity
- O(n + k log k)
  - `n` = size of the array.
  - `k` = number of distinct elements.
  - Frequency counting takes `O(n)` and sorting takes `O(k log k)`.

### 🔹 Space Complexity
- O(k)
  - Additional space is used for the hash map and vector storing frequency-value pairs.

### 🔹 Concepts Used
- Hash Map (`unordered_map`)
- Frequency Counting
- Custom Comparator
- Sorting
- Vector of Pairs

### Solution
```cpp
class Solution {
public:
    vector<int> frequencySort(vector<int>& arr) {
        vector<int>ans;
        unordered_map<int,int>m;
        for(auto x:arr)m[x]++;
        pair<int,int>p;
        vector<pair<int,int>>temp; // pair<freq,calue>
        for(auto x:m){
            p.first=x.second;
            p.second=x.first;
            temp.push_back(p);
        }
        sort(temp.begin(),temp.end(), [](const auto&a, const auto&b){
            if(a.first == b.first){
                return a.second > b.second;
            }
            return a.first < b.first;
        });

        for(auto x:temp){
            for(int i=0;i<x.first;i++){
                ans.push_back(x.second);
            }
        }
        return ans;
    }
};
```

## Problem 3: Sort the People

### 🔹 Topic
- Arrays
- Sorting
- Pair STL

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Created a vector of pairs where each pair stored a person's height and corresponding name.
- Traversed both input arrays and populated the pair vector as `(height, name)`.
- Sorted the vector in descending order of height using a custom comparator.
- Traversed the sorted vector and updated the `names` array with names in sorted order.
- Returned the reordered `names` array.

### 🔹 Time Complexity
- O(n log n)
  - Sorting the vector of pairs dominates the overall complexity.

### 🔹 Space Complexity
- O(n)
  - Additional space is used to store the vector of `(height, name)` pairs.

### 🔹 Concepts Used
- Vector of Pairs
- Custom Comparator
- Sorting
- Array Traversal

### Solution
```cpp
class Solution {
public:
    vector<string> sortPeople(vector<string>& names, vector<int>& heights) {
        int n=names.size();
        vector<pair<int,string>>temp(n);
        for(int i=0;i<n;i++){
            temp[i].first=heights[i];
            temp[i].second=names[i];
        }
        sort(temp.begin(),temp.end(), [](const auto&a, const auto&b){
            return a.first > b.first;
        });

        for(int i=0;i<n;i++){
            names[i]=temp[i].second;
        }

        return names;
    }
};
```

## Problem 4: Sort the Students by Their Kth Score

### 🔹 Topic
- Arrays
- Sorting
- Custom Comparator

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Observed that students need to be sorted based on their `k`th score in descending order.
- Applied the STL `sort()` function directly on the 2D vector.
- Used a custom comparator (lambda function) to compare the `k`th score of two students.
- Placed the student with the higher `k`th score before the other.
- Returned the sorted 2D array.

### 🔹 Time Complexity
- O(n log n)
  - Sorting `n` students dominates the overall complexity.

### 🔹 Space Complexity
- O(log n)
  - Auxiliary space used internally by the STL sorting algorithm (recursive stack).

### 🔹 Concepts Used
- 2D Arrays
- STL `sort()`
- Lambda Function
- Custom Comparator

### Solution
```cpp
class Solution {
public:
    vector<vector<int>> sortTheStudents(vector<vector<int>>& score, int k) {
        sort(score.begin(), score.end(), [k](const auto&a, const auto&b){
            return a[k] > b[k];
        });

        return score;
    }
};
```



