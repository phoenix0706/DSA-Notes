# First Unique Character in a String

Given a string `s`, find the first non-repeating character in it and return its index. If it does not exist, return `-1`.

[Problem Link-Leetcode](https://leetcode.com/problems/first-unique-character-in-a-string/description/)

```
Example 1:

Input: s = "leetcode"
Output: 0
Example 2:

Input: s = "loveleetcode"
Output: 2
Example 3:

Input: s = "aabb"
Output: -1

```

---

## **Intution**:

The problem requires us to find the first non-repeating character in a given string s and return its index. If no such character exists, we return -1. The intuition behind this problem is to efficiently identify the first character that does not repeat itself among all characters in the string.

Understanding the problem can be broken down into the following steps:

1. Traverse the string to identify character frequencies.
2. Traverse the string again to find the first character with a frequency of one.

## **Approach**:

## **Solution**:

### **Brute Force**:

The brute force approach involves checking each character and counting its occurrences in the string. The first character with a count of one is our answer.

### Java

```Java
class Solution {
    public int firstUniqChar(String s) {
        int maxcount=-1;
        int idx=-1;
        for(int i=0;i<s.length();i++){
        int count =0;
        boolean unique=true;

        for(int j=0;j<s.length();j++){
            if(s.charAt(i)==s.charAt(j)&& i!=j){
                unique=false;
                break;
            }
        }
            if (unique){
                return i;
            }

        }
        return -1;
        }
}

```

Time Complexity: O(n^2)

Space Complexity O(1)

---

### **Best Approach**

1. USe hashmap to store frequency of each character in string.
2. Now iterate through the string and check if the count of character is 1. If yes then return the curr index.
3. If no such character have count 1 return -1.

#### Java

```Java
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> map=new HashMap<>();

        for(int i=0;i<s.length();i++){
           char ch = s.charAt(i);
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
           // Find the first unique character
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (map.get(ch) == 1) {
                return i; // Return the index of the first unique character
            }
        }

        return -1;
    }
}
```

#### Python

```python

class Solution:
    def firstUniqChar(self, s: str) -> int:
        map={}
        for char in s:
            map[char]=map.get(char,0)+1
        for i in range(0,len(s)):
            if(map[s[i]]==1):
                return i
        return -1


```

Time Complexity: O(n)

Space Complexity O(n)

---

**Materials To Read/Watch**
