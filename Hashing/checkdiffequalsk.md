# Count All (i,j) pairs such that b[i] - b[j] == k (count of such pairs.) [i<j]

Problem: Count All (i,j) pairs such that b[i] - b[j] == k (count of such pairs.) [i<j]

---

```
Example-1:

Input: b=[1,5,7,-1,5] , k=6


Output: 1


(b[1] - b[3] = 5 - (-1) = 6) -> count = 1


```

## **Solution**:

### **Brute Force**:

The brute force solution involves checking all possible pairs and counting those that satisfy the condition. For checking all possible pairs we're using two loops.

### Dry Run

```
i = 0:
    (b[0] - b[1] = 1 - 5 = -4)
    (b[0] - b[2] = 1 - 7 = -6)
    (b[0] - b[3] = 1 - (-1) = 2)
    (b[0] - b[4] = 1 - 5 = -4)
i = 1:
    (b[1] - b[2] = 5 - 7 = -2)
    (b[1] - b[3] = 5 - (-1) = 6) -> count = 1
    (b[1] - b[4] = 5 - 5 = 0)
i = 2:
    (b[2] - b[3] = 7 - (-1) = 8)
    (b[2] - b[4] = 7 - 5 = 2)
i = 3:
    (b[3] - b[4] = -1 - 5 = -6)


```

### Java

```java

public class Solution {

    static void count_pairs_brute(int[] b, int k) {
        int count = 0;
        for (int i = 0; i < b.length; i++) {
            for (int j = i + 1; j < b.length; j++) {
                if (b[i] - b[j] == k) {
                    count++;
                }
            }
        }
        System.out.println("Count of pairs with diff " + k + " is: " + count);
    }
}


```

Time Complexity: O(n^n)

Space Complexity O(1)

---

### **Best Approach**

We cuse a hash map to store the frequency of elements.
key-->value
element--->frequency of element

Maths logic:
b[i]-b[j]=k
then b[i]=k+b[j]
Suppose if run a loop j=0 to n
then we compute b[i] as k+b[j]
we need to check if b[i] is already present in hashmap if yes then we got the pair where b[i]-b[j] =k . We store frequency of every element as value because suppose if b[i] is present two times then the count should incremented by 2.

**In general terms**

Instead of running 2 Nested For loops, we will create a Hashmap to Store the occurences of the elements which we have encountered in the past. At each index i, we will calculate the Required Element, = (arr[i]+k), we will check if it is present in hashmap, we will do cnt = cnt + freq[requiredElement]. We will update the frequency for current element in hashmap.

### Dry Run

```
Value = 1:
    Complement = 1 + 6 = 7
    freq_map: {1: 1}
Value = 5:
    Complement = 5 + 6 = 11
    freq_map: {1: 1, 5: 1}
Value = 7:
    Complement = 7 + 6 = 13
    count = 0
    freq_map: {1: 1, 5: 1, 7: 1}
Value = -1:
    Complement = -1 + 6 = 5
    count = 1
    freq_map: {1: 1, 5: 1, 7: 1, -1: 1}
Value = 5:
    Complement = 5 + 6 = 11
    count = 1
    freq_map: {1: 1, 5: 2, 7: 1, -1: 1}

```

#### Java

```Java

   static int countPairsWithDiff(int[] b, int k) {
        int count = 0;
        Map<Integer, Integer> seen = new HashMap<>();

        for (int j = 0; j < b.length; ++j) {
            int complement = k + b[j];
            if (seen.containsKey(complement)) {
                count++;
            }
            seen.put(b[j], j);
        }

        return count;
    }

```

#### Python

```python

def count_pairs(b,k):
    freqmap={}
    count=0
    for j in range(0, len(b)):
        complement=k+b[j]
        if complement in freqmap:
            count+=freqmap[complement]
        freqmap[b[j]]=freqmap.get(b[j],0)+1
    print(f"Number of pairs with sum {k} is {count}")


```

Time Complexity: O(n)

Space Complexity O(n)

---

**Materials To Read/Watch**
