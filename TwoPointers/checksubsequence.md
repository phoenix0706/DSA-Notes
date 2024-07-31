# Is Subsequence

Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not)

[Problem Link-Leetcode](https://leetcode.com/problems/is-subsequence/description/)

```
Example 1:

A = “utyuyty”
B = “yyt”
Output= Yes

Example 2:

A = “gg”
B = “ik”
Output= No

Example 3:

Input: s = "abc", t = "ahbgdc"
Output: true
Example 4:

Input: s = "axc", t = "ahbgdc"
Output: false

```

---

## **Approach**:

Using Two pointers travel both the strings.

## **Solution**:

1. Intialise two pointers i=0, j=0
2. Run a while loop `while(i<(len A) && j<(len B))`
3. inside while loop if `A[i]==B[j]` then do `i++`, `j++`
4. If character doesnt matches that is if `A[i]!=B[j]` then we can increment `i++ to match current character at j with next character of A .
5. Now when the loop ends we check wether `j==len(B)` If yes it means we found the entire string B in string A return `True`
6. If we couldn't reach till end of string B it means the character is not present in string A return `False`

### Dry Run

```

   0 1 2 3 4 5 6 7
A= h h h i b b m d
   i

   0  1 2
b= i m d
   j
 We need to find i(0) in string A

 i=0, j=0 A[i]=h h!=i hence i++

 i=1, j=0 A[i]=h h!=i hence i++

 i=2  j=0 A[i]=h h!=i hence i++

 i=3 j=0  A[3]=i i==i
 since both match so we'll find next character of string B in string A.
 Therefore,  i also we'll increment so i++, j++ both

 i=4, j=1 A[4]=b b!=m hence i++

 i=5, j=1 A[5]=b b!=m hence i++

 i=6 j=1  A[6]=m m==m hence i++, j++

 i=7 j=2  A[7]=d d==d hence i++,j++

 i=8, j=3 hence stop

```

#### Java

```Java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int i=0;
        int j=0;
        while (i<s.length() && j<t.length()){
            if(s.charAt(i)==t.charAt(j)){
                i++;
            }
            j++;
        }
        if (i==s.length()){
            return true;
        }
        return false;
    }
}

```

#### Python

```python

class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i=0
        j=0
        while(i<len(s) and j<len(t)):
            if(s[i]==t[j]):
                i+=1
            j+=1
        return i==len(s)


```

Time Complexity: O(n+m)

Space Complexity O(1)

---

**Materials To Read/Watch**

1. [C++ Solution](https://leetcode.com/problems/two-sum/solutions/4529514/optimal-solution-c-hashing)
