# Find count of shortest/largest subarrays with sum k in given array

Given an array of integers nums and an integer k, return the total number of largest/shortest subarrays with sum k subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

```
Example 1:

Input: nums = [1,2,3,4,2,5], k = 5
Output:
Max Length: 2 Count: 1
Min Length: 1 Count: 1


```

---

## **Solution**:

### **Brute Force**:

Use 2 Nested For loops, i will denote starting point of subarray and j will denote point of subarray, now we will check if sum of elements of current subarray is equal to k, we will compare its length with maxSize and minSize and update the count Accordingly

### Java

```Java

public class Solution {

    public static int countShortestSubarraysWithSumK(int[] nums, int k) {
        int n = nums.length;
        int minLength = Integer.MAX_VALUE, count = 0;

        for (int start = 0; start < n; start++) {
            int sum = 0;
            for (int end = start; end < n; end++) {
                sum += nums[end];
                if (sum == k) {
                    int length = end - start + 1;
                    if (length < minLength) {
                        minLength = length;
                        count = 1;
                    } else if (length == minLength) {
                        count++;
                    }
                }
            }
        }

        return count;
    }

    public static int countLargestSubarraysWithSumK(int[] nums, int k) {
        int n = nums.length;
        int maxLength = 0, count = 0;

        for (int start = 0; start < n; start++) {
            int sum = 0;
            for (int end = start; end < n; end++) {
                sum += nums[end];
                if (sum == k) {
                    int length = end - start + 1;
                    if (length > maxLength) {
                        maxLength = length;
                        count = 1;
                    } else if (length == maxLength) {
                        count++;
                    }
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

1. First find the size of the largest and smallest subarray with sum of elements as k using maps. (Refer to the previous problem statement).
2. Now, just count the number of subarrays who have the same size as smallest and largest subarray.

#### Java

```Java


public class Solution {
    static int findmaxlen(int[] arr, int k, int n) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int presum = 0;
        int maxlen = 0;
        for (int i = 0; i < n; i++) {
            presum += arr[i];

            if (presum == k) {
                maxlen = Math.max(maxlen, i + 1);
            } else {
                int x = presum - k;
                if (map.containsKey(x)) {
                    int j = map.get(x);
                    maxlen = Math.max(maxlen, i - j);
                }
            }
            if (!map.containsKey(presum)) {
                map.put(presum, i);
            }

        }
        return maxlen;
    }

    static int findminlen(int[] arr, int k, int n) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int presum = 0;
        int minlen = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            presum += arr[i];

            if (presum == k) {
                minlen = Math.min(minlen, i + 1);
            } else {
                int x = presum - k;
                if (map.containsKey(x)) {
                    int j = map.get(x);
                    minlen = Math.min(minlen, i - j);
                }
            }

            map.put(presum, i);

        }
        return minlen;
    }

    static int findcount(int arr[], int k, int targetlen) {

        if (targetlen == 0) {
            return 0;
        }
        int count = 0;
        int windowSum = 0;
        for (int j = 0; j < targetlen; j++) {
            windowSum += arr[j];
        }
        if (windowSum == k) {
            count++;
        }
        for (int j = targetlen; j < arr.length; j++) {
            windowSum += arr[j] - arr[j - targetlen];
            if (windowSum == k) {
                count++;
            }

        }
        return count;
    }
        public static void main(String[] args) {
        int n = 6;
        int k = 5;
        int[] arr = { 1, 2, 3, 4, 2, 5 };
        int maxlen = findmaxlen(arr, k, n);
        int minlen = findminlen(arr, k, n);
        int maxCount = findcount(arr, k, maxlen);
        int minCount = findcount(arr, k, minlen);
        System.out.println("Max count is " + maxCount + " and max len is " + maxlen + " min count is " + minCount
                + " min len is " + minlen);

    }
}



```

#### Python

```python

def find_max_len(arr, target_sum, n):
    prefix_sum_map = {}
    prefix_sum = 0
    max_length = 0

    for i in range(n):
        prefix_sum += arr[i]

        if prefix_sum == target_sum:
            max_length = max(max_length, i + 1)
        else:
            difference = prefix_sum - target_sum
            if difference in prefix_sum_map:
                j = prefix_sum_map[difference]
                max_length = max(max_length, i - j)

        if prefix_sum not in prefix_sum_map:
            prefix_sum_map[prefix_sum] = i

    return max_length

def find_min_len(arr, target_sum, n):
    prefix_sum_map = {}
    prefix_sum = 0
    min_length = float('inf')

    for i in range(n):
        prefix_sum += arr[i]

        if prefix_sum == target_sum:
            min_length = min(min_length, i + 1)
        else:
            difference = prefix_sum - target_sum
            if difference in prefix_sum_map:
                j = prefix_sum_map[difference]
                min_length = min(min_length, i - j)

        prefix_sum_map[prefix_sum] = i

    return min_length

def find_count(arr, target_sum, target_length):
    if target_length == 0:
        return 0

    count = 0
    window_sum = sum(arr[:target_length])

    if window_sum == target_sum:
        count += 1

    for j in range(target_length, len(arr)):
        window_sum += arr[j] - arr[j - target_length]
        if window_sum == target_sum:
            count += 1

    return count

if __name__ == "__main__":
    n = 6
    target_sum = 5
    arr = [1, 2, 3, 4, 2, 5]

    max_length = find_max_len(arr, target_sum, n)
    min_length = find_min_len(arr, target_sum, n)
    max_count = find_count(arr, target_sum, max_length)
    min_count = find_count(arr, target_sum, min_length)

    print(f"Max count is {max_count} and max length is {max_length}")
    print(f"Min count is {min_count} and min length is {min_length}")



```

Time Complexity: O(n)

Space Complexity O(n)

---

**Materials To Read/Watch**

1. [GfG: Longest subarray having sum k](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)
2. [Another good explanation !](https://takeuforward.org/arrays/longest-subarray-with-sum-k-postives-and-negatives/)
3. [Watch this video ](https://youtu.be/frf7qxiN2qU?feature=shared)
