##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Strings
---

# DSA Problems Solved 

## Problem 1: Rotate String

### 🔹 Topic
- Strings
- String Manipulation
- Simulation

### 🔹 Difficulty
- Easy

### 🔹 Approach
- Created a helper function to perform one left rotation on the string.
- In each rotation, stored the first character, shifted all remaining characters one position to the left, and placed the first character at the end.
- Repeated this rotation operation up to `n` times, where `n` is the length of the string.
- After every rotation, compared the rotated string with the target string.
- Returned `true` if both strings matched at any stage; otherwise returned `false`.

### 🔹 Time Complexity
- O(n²)
  - Each rotation takes `O(n)` time and can be performed up to `n` times.

### 🔹 Space Complexity
- O(1)

### 🔹 Concepts Used
- String Rotation
- Character Shifting
- Simulation

### Solution
```cpp
class Solution { 
    void rot(string &s){
        char t=s[0];
        for(int i=1;i<s.size();i++){
            s[i-1]=s[i];
        }
        s[s.size()-1]=t;
    }
public:
    bool rotateString(string s, string goal) {
        for(int i=0;i<s.size();i++){
            rot(s);
            if(s==goal)return true;
        }
        return false;
    }
};
```

## Problem 2: Reverse Words in a String

### 🔹 Topic
- Strings
- Parsing
- Simulation

### 🔹 Difficulty
- Medium

### 🔹 Approach
- Ignored leading spaces by advancing the pointer to the first non-space character.
- Traversed the string and built each word character by character using a temporary string.
- Whenever a space was encountered, stored the completed word in a vector and cleared the temporary string.
- After the traversal, added the last word to the vector if it existed.
- Constructed the final answer by traversing the vector in reverse order.
- Inserted a single space between consecutive words while building the result to avoid extra spaces.

### 🔹 Time Complexity
- O(n)
  - The string is traversed once to extract words and once more to construct the reversed sentence.

### 🔹 Space Complexity
- O(n)
  - Additional space is used to store the extracted words and the final output string.

### 🔹 Concepts Used
- String Traversal
- Word Extraction
- Vector
- Reverse Iteration
- Handling Extra Spaces

### Solution
```cpp
class Solution {
public:
    string reverseWords(string s) {
        string temp="";
        string ans="";
        vector<string>arr;
        int n=s.size(),i=0;
        while(i<n && s[i]==' '){
            i++;
        }
        while(i<n){
            if(s[i]==' '){
              if(temp.size())arr.push_back(temp);
              temp.clear();
            }else{
                temp+=s[i];
            }
            i++;
        }
        if(temp.size()){
            arr.push_back(temp);
            temp.clear();
        }
        for(int i=arr.size()-1;i>=0;i--){
            for(auto x:arr[i])ans+=x;
            if(i>0)ans+=' ';
        }
        return ans;
    }
};
```