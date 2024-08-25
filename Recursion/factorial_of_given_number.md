# Factorial of a given number

Given an integer n, return the factorial of n.

Factorial of a non-negative integer, is the multiplication of all integers smaller than or equal to n (use 64-bits to return answer).

[Problem Link]()

```

Example 1

Input : n = 3
Output : 6
Explanation : Factorial = 1 * 2 * 3 => 6

Example 2

Input : n = 5
Output : 120
Explanation : Factorial = 1 * 2 * 3 * 4 * 5 => 120

Example 3

Input : n = 1
Output :
1

```

---

## **Approach**:

1. Define a function that calculates the factorial of a number.
2. In the function, if the number is 0 or 1, return 1 (base case).
3. Otherwise, return the number multiplied by the factorial of the number minus 1 (recursive case).

![alt text](image-1.png)

## **Solution**:

#### Java

```Java

class Solution {
    public int factorial(int n) {
        // Base case: factorial of 0 or 1 is 1
        if (n <= 1) return 1;
        // Recursive case: n * factorial of n-1
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int N = 5; // Example input
        System.out.println("Factorial of " + N + " is " + solution.factorial(N));
    }
}



```

#### Python

```python


```

Time Complexity: O(N) — The function makes N recursive calls to reach the base case, so the time complexity is proportional to the number of recursive calls

Space Complexity : O(N) — The call stack grows with each recursive call, using N stack frames, so the space complexity is proportional to the depth of recursion.

---

**NOTE: For very large numbers, recursion can lead to a stack overflow due to too many nested function calls.**

**Materials To Read/Watch**
