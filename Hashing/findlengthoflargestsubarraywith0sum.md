# Find the length of largest subarray with 0 sum

Given an array arr[] of length N, find the length of the longest sub-array with a sum equal to 0.

[Problem Link-GFG](https://www.geeksforgeeks.org/find-the-largest-subarray-with-0-sum/)

```
Example1:

Input: arr[] = {15, -2, 2, -8, 1, 7, 10, 23}
Output: 5
Explanation: The longest sub-array with elements summing up-to 0 is {-2, 2, -8, 1, 7}

Example2:

Input: arr[] = {1, 2, 3}
Output: 0
Explanation: There is no subarray with 0 sum

Example3:

Input:  arr[] = {1, 0, 3}
Output:  1
Explanation: The longest sub-array with elements summing up-to 0 is {0}

```

---

## **Approach**:

## **Solution**:

### **Brute Force**:

Consider all sub-arrays one by one and check the sum of every sub-array. If the sum of the current subarray is equal to zero then update the maximum length accordingly. After iterating over all the subarrays, return the maximum length.

### Java

```Java

class Solution {
    static int maxLen(int arr[], int N)
    {
        int max_len = 0;
        for (int i = 0; i < N; i++) {
            int curr_sum = 0;
            for (int j = i; j < N; j++) {
                curr_sum += arr[j];
                if (curr_sum == 0)
                    max_len = Math.max(max_len, j - i + 1);
            }
        }
        return max_len;
    }

```

Time Complexity: O(N^2)

Space Complexity : O(1)

---

### **Best Approach**

1. Use Hashmap to store the prefix sum.
2. Iterate through the hashmap and check two things.
   1. If the curr prefix sum is - then length will be `i+1`.
   2. If the prefix sum is already presnt in the hashmap then length will be `i-map[pre_sum] +1`
3. Compare length with max length and update max length accordingly

#### Java

```Java


class GfG
{
    int maxLen(int arr[], int n)


    {
        HashMap<Integer, Integer> map=new HashMap<>();
        int sum=0;
        int ans=0;
    for(int i=0;i<n;i++){
        sum=sum+arr[i];
        if(map.containsKey(sum)){
           int idx= map.get(sum)+1;
           ans=Math.max(ans, i-idx+1);
        }
        else if (sum==0){
            ans=Math.max(ans,i+1);
        }
        else{
            map.put(sum,i);
        }


    }
        return ans;
    }
}

```

#### Python

```python

class Solution:
    def maxLen(self, n, arr):
        maxlen=0
        presum=0
        hash_map={}
        for i in range (0, len(arr)):
            presum+=arr[i]
            if hash_map.get(presum,-1)!=-1:
                idx=hash_map[presum]+1
                maxlen=max(maxlen,i-idx+1)
            elif presum==0:
                maxlen=max(maxlen, i+1)
            else:
                hash_map[presum]=i
        return maxlen



```

Time Complexity: O(n)
Space Complexity O(n)

---

**Materials To Read/Watch**

1. [Read best blog here](https://www.geeksforgeeks.org/find-the-largest-subarray-with-0-sum/)
