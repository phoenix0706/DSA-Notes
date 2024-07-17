# Max Portfolio from Stocks

In a fictional stock market, fund managers are required to ch
portfolios by including stocks from different industries.
Given an array, stocks, where the stocks[i] represent the number of companies in the ith industry. The task is to distribute stocks in such a way that each portfolio has exactly k distinct types of stocks where kis a given integer and each company is included only once in a portfolio.
Find the maximum number of portfolios that can be created.
Input Format
The first line contains an integer k, that represents the distinct kinds of stocks that each portfolio must have.
The second line contains an integer n, that represents the different kinds of stocks.
The next n lines represent stocks[i] that represent the count of stocks of the kind i.

[Problem Link](https://www.desiqna.in/9717/de-shaw-oa-sde-set-55-kumar-k)

```
Example
k=2, n=3, stocks = [3, 3, 3].

Each portfolio must have 2 kinds of stocks (as k = 2).
One of the optimal methods can be:
• Portfolio 1 gets stocks of kinds 1 and 2.
• Portfolio 2 gets stocks of kinds 1 and 3.
• Portfolio 3 gets stocks of kinds 2 and 3.
• Portfolio 4 gets stocks of kinds 1 and 2

```

---

## **Approach**:

1. We have `n` types of items. stocks[i] tells frequency of item i.
2. We need to make group of k distinct items.
3. Final output should contain maximum such kinds of groups that can be formed.
4. If we want to make y groups of size "k" then sum of the array should be `sum(array)>=y*k`.

## **Solution**:

### **Brute Force**:

1. Let's suppose maximum no of portfolios is depicted by variable `y` . Means maximum `y` no of portfolios can be formed that have k distinct stocks
2. We'll try for `y=1` If it is possible then try for `y=2` and so on. We'll reach a point say `y=6` we see it is not possible to create 6 portfolios that have k distinct types of stocks therefore we stop at `y=5`.
   Graph

```
YYYYYNNNNNNNNNNNNNNNNNNNNNNNNNN

```

3. As we need to find last occurence of `y` But still we don't know how to check if we "y" groups are possible or not.

**Logic to find "Y" groups possible or not**

1.  Sort frequencies in decreasing order.
    if we're trying for say `y=4`
    check whenever `stocks[i]>=y` simply do `count++`.

```Java
class FinanceStocks {

    static boolean check(long i, int k, int[] stocks, int n) {
        long t = i * k;
        int j = 0;
        while (j < n) {
            if (stocks[j] > t) {
                t = t - i;

            } else {
                t = t - stocks[j];
            }
            j += 1;
        }
        if (t <= 0) {
            return true;
        }
        return false;

    }

    static void maxPortfolio(int[] stocks, int n, int k) {
        long answer = -1;
        long sum = 0;
        for (int j = 0; j < n; j++) {
            sum += stocks[j];
        }
        long i = 1;
        while (i <= sum) {
            if (!check(i, k, stocks, n)) {
                answer = i - 1;
                break;
            } else {
                i += 1;
            }
        }
        System.out.println(answer);

    }

    public static void main(String[] args) {
        int n = 3;
        int k = 2;
        int stocks[] = { 3, 3, 3 };
        maxPortfolio(stocks, n, k);
    }
}
```

Time Complexity: O(Sum\*N)

Space Complexity O(1)

---

### **Best Approach**

1.  As we sort array in decreasing order first and we need to find last occurence of the `y` (check the graph)
    we can simply apply Binary search!
2.  Initialse low=0 and high=10^18(very big number). Maximum no of portfolio will lie within this range. Use binary search logic of finding last occurence of an element.

```
Graph:

YYYYYNNNNNNNNNNNNNNNNNNNNNNNNNN

```

#### Java

```Java
import java.util.*;
import java.io.*;
import java.math.*;

class FinanceStocks2 {

    static boolean check(long i, int k, int[] stocks, int n) {
        long t = i * k;
        int j = 0;
        while (j < n) {
            if (stocks[j] > t) {
                t = t - i;

            } else {
                t = t - stocks[j];
            }
            j += 1;
        }
        if (t <= 0) {
            return true;
        }
        return false;

    }

    static void maxPortfolio(int[] stocks, int n, int k) {
        long answer = -1;
        long low = 1;
        long high = (long) Math.pow(10, 18);
        long foundans = 0;
        while (low <= high && foundans == 0) {
            long mid = (low + high) / 2;
            if (check(mid, k, stocks, n) == true && check(mid + 1, k, stocks, n) == false) {
                answer = mid;
                foundans = 1;
            } else if (check(mid, k, stocks, n) == true) {
                low = mid;
            } else {
                high = mid - 1;
            }
        }
        System.out.println(answer);

    }

    public static void main(String[] args) {
        int n = 3;
        int k = 2;
        int stocks[] = { 3, 3, 3 };
        maxPortfolio(stocks, n, k);
    }
}
```

#### Python

Time Complexity: O(log(sum)\*N)

Space Complexity O(1)

---
