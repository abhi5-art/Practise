##  Daily Progress Overview 

Today's preparation :
- Data Structures & Algorithms : Binary Number,String
- Core Subject Preparation : Database Management System 

---

# DSA Problems Solved 

## Problem 1:  Exactly One Consecutive Set Bits Pair

- **Platform:** : Leetcode
- **Topic:** Binary Representation 
- **Difficulty:** Easy
- **Concepts Used:**
  - Binary Representation 

### 🔹 Approach
- Converted the given number into its binary representation and stored the bits in a vector.
- Traversed the binary representation and checked every adjacent pair of bits.
- Counted the number of occurrences where two consecutive bits were both set (`1`).
- Returned `true` only if exactly one consecutive set bits pair was present; otherwise returned `false`.
- Handled small values (`n < 2`) separately since they cannot contain a pair of consecutive set bits.

### 🔹 Time Complexity
- O(log n)
  - The number is traversed once to generate its binary representation and once to count consecutive set bit pairs.

### 🔹 Space Complexity
- O(log n)
  - Additional space is used to store the binary representation of the number.

### Solution
```cpp
class Solution {
public:
    bool consecutiveSetBits(int n) {
        vector<bool>temp;
        if(n<2)return 0;
        while(n>0){
            temp.push_back(n%2);
            n/=2;
        }
        int cnt=0;
        for(int i=0;i<temp.size()-1;i++)if(temp[i]==1 && temp[i+1]==1)cnt++;

        return cnt==1;
    }
};
```

## Problem 2:  Rotate String

- **Platform:** : Leetcode
- **Topic:** - Strings, String Manipulation
- **Difficulty:** Easy

### 🔹 Concepts Used
- String Rotation
- Character Shifting
- Simulation

### 🔹 Approach
- Created a helper function to perform one left rotation on the string.
- In each rotation:
  - Stored the first character.
  - Shifted all remaining characters one position to the left.
  - Placed the first character at the end of the string.
- Repeated the rotation operation up to `n` times, where `n` is the length of the string.
- After every rotation, compared the rotated string with the target string.
- Returned `true` if both strings matched at any point; otherwise returned `false`.

### 🔹 Time Complexity
- O(n²)
  - Each rotation takes `O(n)` time.
  - Up to `n` rotations may be performed.

### 🔹 Space Complexity
- O(1)
  - Rotation is performed in-place without using additional data structures.

### Solution
```cpp
class Solution {
    void rotate(string &str){
        char c=str[0];
        for(int i=1;i<str.size();i++){
            str[i-1]=str[i];
        }
        str[str.size()-1]=c;
    }
public:
    bool rotateString(string s, string goal) {
        for(int i=0;i<s.size();i++){
            rotate(s);
            if(s==goal)return 1;
        }
        return 0;
    }
};
```