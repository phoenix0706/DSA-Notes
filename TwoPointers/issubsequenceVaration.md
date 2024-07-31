# Is Subsequence-Variation

### Asked in Google OA.

[Problem Link](https://www.desiqna.in/17545/google-oa-first-subsequence-13th-july)

```

Example 1:

A = “acbca”
B = "cba"
Output= 1

Example 2:

A = "lhs"
B = "rhs"
Output= -1


```

---

## **Approach**:

Using Two pointers travel both the strings.

## **Solution**:

1. Make a function called issubsequence code.

   1. Intialise two pointers i=0, j=0, count=0.
   2. Run a while loop `while(i<(len A) && j<(len B))`
   3. inside while loop if `A[i]==B[j]` and check if `count==0` then store `p=j`. Further increment `i++`, `j++`, `count++`.
   4. If character doesnt matches that is if `A[i]!=B[j]` then we can increment `i++` to match current character at j with next character of A . x
   5. Now when the loop ends we check wether `j==len(B)` If yes it means we found the entire string B in string A return `True`
   6. If we couldn't reach till end of string B it means the character is not present in string A return `False`

2. Now for each char at index `j` can be changed from `a` to `z`-> only 26 options for each index `j`. hence try all possible 26 combinations string.

3. O(n-1)\*26 possible strings. out of all of them one whichever gives yes is answer.

4. if is_subsequence() function returns true store `answer=p+1`.

#### Java

```Java

import java.util.Scanner;

public class Main {
    private static int p = -1;

    public static boolean isSubsequence(String A, String B) {
        int n = A.length();
        int m = B.length();
        int i = 0, j = 0, count = 0;

        while (i < m && j < n) {
            if (A.charAt(j) == B.charAt(i)) {
                if (count == 0) {
                    p = j;
                }
                i++;
                j++;
                count++;
            } else {
                j++;
            }
        }

        return count == m;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int t = scanner.nextInt();
        scanner.nextLine();
        for (int test = 0; test < t; test++) {
            String a = scanner.nextLine();
            String b = scanner.nextLine();
            int answer = -1;

            for (int i = 1; i < b.length(); i++) {
                for (char c = 'a'; c <= 'z'; c++) {
                    StringBuilder r = new StringBuilder(b);
                    r.setCharAt(i, c);
                    p = -1;
                    if (isSubsequence(a, r.toString())) {
                        answer = p ;
                    }
                }
            }
            System.out.println(answer);
        }
        scanner.close();
    }
}


```

#### Python

```python

global idx
idx=-1
answer=-1
def isSubsequence(s: str, t: str) -> bool:
    i=0
    j=0
    count=0
    while(i<len(s) and j<len(t)):
        if(s[i]==t[j]):
            if count ==0:
                global idx
                idx=j
            i+=1
            count+=1
        j+=1
    return i==len(s)
s="cbd"
t="acbcba"
for i in range(1,len(s)):
    for char in "abcdefghijklmnopqrstuvwxyz":
        string=s
        string=s[:i]+char+s[i+1:]
        if(isSubsequence(string,t)):
            answer=idx
print(answer)



```

Time Complexity: O(m*(n+m)*26)

Space Complexity O(1)

---

**Materials To Read/Watch**
