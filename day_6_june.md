##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Strings
- Core Subject Preparation : Operating System

---

# DSA Problems Solved 

## Problem 1:  Isomorphic Strings

- **Platform:** : Leetcode
- **Topic:** String, Hashmap
- **Difficulty:** Easy

### 🔹 Approach
- Used an unordered map to store the mapping from characters of the first string to characters of the second string.
- Used an unordered set to track characters of the second string that had already been mapped.
- Traversed both strings simultaneously.
- If a character from the first string had not been seen before:
  - Checked whether the corresponding character in the second string was already mapped.
  - If yes, the mapping was invalid.
  - Otherwise, created a new mapping and marked the character as used.
- If a character from the first string was already mapped:
  - Verified that it mapped to the current character in the second string.
  - If not, returned false.
- If all mappings remained consistent throughout the traversal, returned true.

### 🔹 Time Complexity
- O(n)

### 🔹 Space Complexity
- O(n)

### 🔹 Concepts Used
- Hash Map (`unordered_map`)
- Hash Set (`unordered_set`)
- Character Mapping
- One-to-One Correspondence



### Solution
```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char,char>m;
        unordered_set<char>st;
        for(int i=0;i<s.size();i++){
            if(m.find(s[i]) == m.end()){
                if(st.count(t[i]))return 0;
                else{
                    m[s[i]]=t[i];
                    st.insert(t[i]);
                }
            }else{
                if(m[s[i]] != t[i])return 0;
            }
        }

        return 1;
    }
};
```

## Problem 2:   Valid Anagram

- **Platform:** : Leetcode
- **Topic:** - - Strings, Hashing, Frequency Counting
- **Difficulty:** Easy

### 🔹 Approach
- Created two maps to store the frequency of characters in both strings.
- Traversed the first string and counted occurrences of each character in the first map.
- Traversed the second string and counted occurrences of each character in the second map.
- Compared both frequency maps.
- If the maps were identical, both strings contained the same characters with the same frequencies and were therefore anagrams.
- Otherwise, returned false.

### 🔹 Time Complexity
- O(n log n)
  - Each insertion/update in `map` takes `O(log n)`.
  - Frequency counting is performed for both strings.

### 🔹 Space Complexity
- O(n)

### 🔹 Concepts Used
- Character Frequency Counting
- Hashing / Mapping
- String Comparison

### Solution
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        map<char,int>m1;
        map<char,int>m2;
        for(auto x:s)m1[x]++;
        for(auto x:t)m2[x]++;
        return m1==m2;
    }
};
```