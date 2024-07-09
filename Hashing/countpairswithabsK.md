# Count Number of Pairs With Absolute Difference K

Given an integer array nums and an integer k, return the number of pairs (i, j) where i < j such that |nums[i] - nums[j]| == k.

The value of |x| is defined as:

x if x >= 0.
-x if x < 0.

[Problem Link-Leetcode](https://leetcode.com/problems/count-number-of-pairs-with-absolute-difference-k/description/)

```
Example 1:

Input: nums = [1,2,2,1], k = 1
Output: 4

Explanation: The pairs with an absolute difference of 1 are:
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]
- [1,2,2,1]



Example 2:

Input: nums = [1,3], k = 3
Output: 0

Explanation: There are no pairs with an absolute difference of 3.


Example 3:

Input: nums = [3,2,1,5,4], k = 2
Output: 3

Explanation: The pairs with an absolute difference of 2 are:
- [3,2,1,5,4]
- [3,2,1,5,4]
- [3,2,1,5,4]


```

---

## **Solution**:

### **Brute Force**:

Use 2 Nested For Loops and for every i, start j from i+1, because j>i(given in problem). Check if Absolute Difference between b[i] and b[j] == k, cnt++. Finally Print this Count of All Valid Pairs.

### Java

```Java

public class Solution {

    public static int countPairs(int[] b, int k) {
        int count = 0;
        int n = b.length;
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                if (Math.abs(b[i] - b[j]) == k) {
                    count++;

                }
            }
        }
        return count;
    }
}

```

Time Complexity: O(n^2)

Space Complexity O(1)

---

### **Best Approach**

General Maths:

```
abs(b[i]-b[j])=k

b[i]-b[j]=k

b[i]=b[j]+k --------------(eqn1)

b[i]-b[j]=-k

b[i]=b[j]-k --------------(eqn2)

```

Traverse array from j=0 to n. For every b[j] count the frequency of how many times b[i] has come.

B[i] will be calculated using following 2 formulas:-

B[i] = b[j] + k
B[i] = b[j] - k

#### Java

```Java

class Solution {
    public int countKDifference(int[] nums, int k) {
        //ele, frequency
        HashMap <Integer,Integer> map=new HashMap<>();
        int count=0;
        for(int i=0;i<nums.length;i++){
            int num1=nums[i]-k;
            int num2=k+nums[i];
            if(map.containsKey(num1)|| map.containsKey(num2)){
                count=count+map.getOrDefault(num1,0)+map.getOrDefault(num2,0);
            }

            int g=map.getOrDefault(nums[i],0);
                map.put(nums[i],g+1);

        }
        return count;
    }
}

```

#### Python

```python

class Solution:
    def countKDifference(self, nums: List[int], k: int) -> int:
        map={}
        count=0
        for ele in nums:
            num1=ele-k
            num2=ele+k
            if num1 in map or num2 in map:
                count=count+ map.get(num1,0)
                count=count+ map.get(num2,0)
            map[ele]=map.get(ele,0)+1
        return count

```

Time Complexity: O(n)

Space Complexity O(n)

---

**Materials To Read/Watch**
