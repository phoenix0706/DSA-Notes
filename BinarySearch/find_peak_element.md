# Find Peak Element

[Detailed indepth explanation](https://takeuforward.org/data-structure/peak-element-in-array/)

A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in O(log n) time.

[Problem Link](https://leetcode.com/problems/find-peak-element/description/)

```

Example 1:
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.

Example 2:
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.


```

---

## **Approach**:

![alt text](image.png)
![alt text](image-1.png)

## **Solution**:

### **Brute Force**:

1. We will start traversing the array and for every index, we will check the below condition.

2. If((i == 0 or arr[i-1] < arr[i]) and (i == n-1 or arr[i] > arr[i+1])): whenever this condition is true for an element, we should return its index.

### Java

```Java




import java.util.*;

public class Solution {
    public static int findPeakElement(ArrayList<Integer> arr) {
        int n = arr.size(); // Size of array.

        for (int i = 0; i < n; i++) {
            // Checking for the peak:
            if ((i == 0 || arr.get(i - 1) < arr.get(i))
                    && (i == n - 1 || arr.get(i) > arr.get(i + 1))) {
                return i;
            }
        }
        // Dummy return statement
        return -1;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr =
            new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 5, 1));
        int ans = findPeakElement(arr);
        System.out.println("The peak is at index: " + ans);
    }
}





```

Time Complexity: O(n)

Space Complexity O(1)

---

### **Best Approach**

1. Check for edge cases first check if array has only 1 element if yes then return idx 0. Another edge case is to check element at start and end. Then take low=1, high=n-2 to avoid overflow cases.
2. Use BS, check if mid >mid+1 and mid>mid-1. if yes you found peak element return mid .
3. If not, Check wether we're standing in left half or right half. If standing at left eliminate it and move to right and vice versa.

How do you eliminate?

- take advantage of sorting
  if arr[mid]<=arr[mid+1] means on left half do low=mid+1
  else
  high=mid-1;

#### Java

```Java

class Solution {
    public int findPeakElement(int[] nums) {
        if(nums.length==1){
            return 0;
        }
        int n=nums.length;
        if(nums[0]>nums[1]){
            return 0;
        }
        if(nums[n-1]>nums[n-2]){
            return n-1;
        }
        int low=1;
        int high=n-1;
        while(low<=high){
            int mid=(low+high)/2;
            if(nums[mid]>nums[mid+1] && nums[mid]>nums[mid-1]){
                return mid;

            }
            else if (nums[mid]<=nums[mid+1]){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        return -1;
    }
}


```

#### Python

```python

class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        start=0
        end=len(nums)-1

        while(start<end):
            mid=start+((end-start)//2)
            if nums[mid]>nums[mid+1]:
                end=mid
            else:
                start=mid+1
        return start


```

Time Complexity: O(logN), N = size of the given array.
Reason: We are basically using binary search to find the minimum.

Space Complexity O(1)

---

**Materials To Read/Watch**

1. [TUF explanation](https://takeuforward.org/data-structure/peak-element-in-array/)
