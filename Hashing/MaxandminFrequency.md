# We are given an Array of Numbers. We have to find and print any Number with Maximum Frequency and Minimum Frequency.

Problem: We are given an Array of Numbers. We have to find and print any Number with Maximum Frequency and Minimum Frequency.

---

```
Example-1:

Input:  arr[] =  [3, 2, 3, 2, 4, 3]

Output: Element is 3, Frequency is 3
        Element is 4, Frequency is 1


Maximum Frequency:- Element is 3, Frequency is 3
Minimum Frequency:- Element is 4, Frequency is 1

Frequencies of Elements of Array are:-

3 - 3
2 - 2
4 - 1



```

## **Solution**:

### **Brute Force**:

Use two nested loops to find maximum and minimum elements in an array.

### Java

```java
public class Solution {

    static void print_max_min_freq_brute(int[] arr) {
        int max_count = 0;
        int min_count = Integer.MAX_VALUE;
        int min_ele = 0, max_ele = 0;

        for (int i = 0; i < arr.length; i++) {
            int count = 0;
            for (int j = 0; j < arr.length; j++) {
                if (arr[i] == arr[j]) {
                    count++;
                }
                if (count > max_count) {
                    max_count = count;
                    max_ele = arr[i];
                }
                if (count < min_count) {
                    min_count = count;
                    min_ele = arr[i];
                }
            }
        }
        System.out.println("Maxm Frequency is " + max_count + " and element is " + max_ele);
        System.out.println("Minm Frequency is " + min_count + " and element is " + min_ele);

    }
}
```

Time Complexity: O(n^n)

Space Complexity O(1)

---

### **Best Approach**

Use Hashmap to Store the Frequencies of Elements where key will be the Array element and Value will be the Frequency of array element and Update our Maximum and Minimum Frequencies Accordingly.

#### Java

```Java
public class Solution{
static void print_max_min_freq(int[] arr) {
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        int key_max = 0, key_min = 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int num = map.getOrDefault(arr[i], 0);
            map.put(arr[i], num + 1);
        }
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int key = entry.getKey();
            int value = entry.getValue();
            if (max < value) {
                max = value;
                key_max = key;
            }
            if (value < min) {
                min = value;
                key_min = key;
            }
        }
        System.out.println("Maxm Frequency is " + max + " and element is " + key_max);
        System.out.println("Minm Frequency is " + min + " and element is " + key_min);
}
    }

```

#### Python

```python

def print_max_min_frequency(arr):
    map={}
    min_count=float('inf')
    max_count=float('-inf')
    min_ele=arr[0]
    max_ele=arr[0]
    for ele in arr:
        if ele not in map:
            map[ele]=1
        else:
            map[ele]+=1
    for key,value in map.items():
        if value>max_count:
            max_count=value
            max_ele=key
        if value<min_count:
            min_count=value
            min_ele=key
    print(f" Max Frequency element is {max_ele} and the frequency is {max_count} \n Min frequency element is {min_ele} and the frequency is {min_count}")

```

Time Complexity: O(nlogn)

Space Complexity O(n)

---

**Materials To Read/Watch**
