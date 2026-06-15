##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Strings
---

# DSA Problems Solved 

## Problem 1: Largest Odd Number in String

### 🔹 Topic
- Strings
- Greedy

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Traversed the string from right to left to find the first odd digit.
- Stored the index of this rightmost odd digit.
- If no odd digit was found, returned an empty string since no odd number could be formed.
- Otherwise, constructed the answer by taking the prefix of the string from the beginning up to the identified index.
- Returned this prefix as the largest odd number present in the string.

### 🔹 Time Complexity
- O(n)
  - One traversal to locate the rightmost odd digit and another traversal to construct the answer.

### 🔹 Space Complexity
- O(n)
  - Additional space is used to store the resulting substring.

### 🔹 Concepts Used
- String Traversal
- Prefix Extraction
- Greedy Observation

### Solution
```cpp
class Solution {
public:
    string largestOddNumber(string str) {
        int n=str.size(),temp=-1;
        string ans="";
        
        for(int i=n-1;i>=0;i--){
            if((str[i]-'0') % 2){
                temp=i;
                break;
            }
        }
        if(temp == -1)return ans;
        for(int i=0;i<=temp;i++){
           ans+=str[i];
        }

        return ans;
    }
};
```

## Problem 2: Longest Common Prefix

### 🔹 Topic
- Strings
- Prefix Matching

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Initialized the answer with the first string in the array.
- Created a helper function to find the common prefix between two strings:
  - Compared characters of both strings from the beginning.
  - Continued adding matching characters to the prefix.
  - Stopped as soon as a mismatch occurred or either string ended.
- Iterated through the remaining strings in the array.
- Updated the current answer by finding the common prefix between the existing answer and the current string.
- After processing all strings, the resulting string represented the longest common prefix.

### 🔹 Time Complexity
- O(n × m)
  - `n` = number of strings.
  - `m` = length of the shortest common prefix (or average string length in the worst case).
  - Each character is compared at most once while updating the prefix.

### 🔹 Space Complexity
- O(m)
  - Additional space is used to store the temporary common prefix string.

### 🔹 Concepts Used
- String Traversal
- Prefix Comparison
- Incremental Reduction


### Solution
```cpp
class Solution {
    string pre(string a,string b){
        int i=0,j=0;
        string ans="";
        while(i<a.size() && j<b.size()){
            if(a[i]==b[j]){
                ans+=a[i];
                i++;j++;
            }else{
                break;
            }
        }
        return ans;
    }
public:
    string longestCommonPrefix(vector<string>& str) {
        int n=str.size();
        string ans=str[0];   
        for(int i=1;i<n;i++){
           ans=pre(ans, str[i]);
        }
        return ans;
    }
};
```