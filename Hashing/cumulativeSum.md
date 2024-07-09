# Cumulative Sum Query

You are given a list of N numbers and Q queries. Each query is specified by two numbers i and j; the answer to each query is the sum of every number between the range [i, j] (inclusive).

Note: the query ranges are specified using 0-based indexing.

[Problem Link-SPOJ](https://www.spoj.com/problems/CSUMQ/)

```
Example 1:

Input:
3
1 4 1
3
1 1
1 2
0 2

Output:
4
5
6



```

---

## **Approach**:

For given array, construct a prefix array of size n, and prefix[i] = prefix[i-1] + arr[i]. After creating this prefix Array.

For any given l and r,
Sum of the elements in arr in the Range of [l … r] = Prefix[r] - prefix[l-1]

## **Solution**:

### **Brute Force**:

For each i and j, start our k pointer from i and go till j for each k, we will update our sum by doing sum = sum + arr[i]. Finally, print this sum.

### Java

```Java


public class Solution {

    static void printsumbrute(int arr[], int i, int j) {
        int sum = 0;
        for (int k = i; k <= j; k++) {
            sum += arr[k];
        }
        System.out.println(sum);
    }
}

```

Time Complexity: O(n^q) For each query the function will be called and array will be iterated.

Space Complexity O(1)

---

### **Best Approach**

1. Prefix Sum Array: The prefix sum array helps us quickly calculate the sum of any subarray. The idea is to preprocess the array such that prefix[i] contains the sum of elements from the start of the array to the i-th element.

```
prefix[i] = array[0] + array[1] + ... + array[i]

```

2. Query Answering: For a given query [i,j], the sum of elements from i to j can be computed as:

```
sum(i, j) = prefix[j] - prefix[i-1]

If i is 0, then  sum(i,j)=prefix[j].


```

#### Java

```Java

import java.util.Scanner;

public class RangeSumQuery {

    public static int[] preprocessPrefixSum(int[] array) {
        int[] prefixSum = new int[array.length];
        prefixSum[0] = array[0];
        for (int i = 1; i < array.length; i++) {
            prefixSum[i] = prefixSum[i - 1] + array[i];
        }
        return prefixSum;
    }

    public static int rangeSumQuery(int[] prefixSum, int i, int j) {
        if (i == 0) {
            return prefixSum[j];
        } else {
            return prefixSum[j] - prefixSum[i - 1];
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int N = scanner.nextInt();
        int[] array = new int[N];
        for (int i = 0; i < N; i++) {
            array[i] = scanner.nextInt();
        }

        int Q = scanner.nextInt();
        int[][] queries = new int[Q][2];
        for (int i = 0; i < Q; i++) {
            queries[i][0] = scanner.nextInt();
            queries[i][1] = scanner.nextInt();
        }

        int[] prefixSum = preprocessPrefixSum(array);

        for (int i = 0; i < Q; i++) {
            int queryResult = rangeSumQuery(prefixSum, queries[i][0], queries[i][1]);
            System.out.println(queryResult);
        }

        scanner.close();
    }
}

```

#### Python

```python

def preprocess_prefix_sum(arr):
    pre_sum=[0]*(len(arr)+1)
    pre_sum[0]=arr[0]
    for i in range(1, len(arr)):
        pre_sum[i]=pre_sum[i-1]+arr[i]
    return pre_sum

def range_sum_query(prefix_sum,i, j):
    if i==0:
        return prefix_sum[j]
    else:

        return prefix_sum[j]-prefix_sum[i-1]
def main():
    n=int(input())
    arr=[int(x) for x in input().split()]


    prefix_sum = preprocess_prefix_sum(arr)
    queries=int(input())
    results = []

    for _ in range(0,queries):
        i, j=[int (q) for q in  input().split()]

        if i<j:
            results.append(range_sum_query(prefix_sum, i, j))
        else:
            results.append(range_sum_query(prefix_sum, j, i))



    for result in results:
        print(result)

if __name__ == "__main__":
    main()

```

Time Complexity: O(n+q)

O(n) for creating Prefix Array
O(q) for Traversing Queries

Space Complexity O(n)
Because of Prefix Array

---

**Materials To Read/Watch**
