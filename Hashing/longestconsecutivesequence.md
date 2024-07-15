# Longest Consecutive Sequence

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in `O(n)` time.

[Problem Link-Leetcode](https://leetcode.com/problems/longest-consecutive-sequence/description/)

```
Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9

```

---

## **Approach**:

## **Solution**:

### **Brute Force**:

1. Iterate through each element in array. Initialise longest=0
2. For every element x find consecutive elements x+1,x+2,x+3.. using linear search algo.
3. If say element x+1 is found increment count and search for x+2 and so on.
4. Compare count with longest

### Java

```Java
public class Solution {
    public static boolean linearSearch(int []a, int num) {
        int n = a.length; //size of array
        for (int i = 0; i < n; i++) {
            if (a[i] == num)
                return true;
        }
        return false;
    }
    public static int longestSuccessiveElements(int []a) {
        int n = a.length; //size of array
        int longest = 1;
        //pick a element and search for its
        //consecutive numbers:
        for (int i = 0; i < n; i++) {
            int x = a[i];
            int cnt = 1;
            //search for consecutive numbers
            //using linear search:
            while (linearSearch(a, x + 1) == true) {
                x += 1;
                cnt += 1;
            }

            longest = Math.max(longest, cnt);
        }
        return longest;
    }
}

```

Time Complexity: O(N^2), N = size of the given array.
Reason: We are using nested loops each running for approximately N times.

Space Complexity : O(1), as we are not using any extra space to solve this problem.

---

### **Best Approach**

1. Create two hashmap one named present other named checked.
2. store every element in present hashmap and mark them True.
3. Now iterate through the array.
4. For every element say `num` in array check wether `num-1` is present in present array and it has not been marked as check. If not it means `num` is the starting number of a subsequence. Store num in `i` and initialse `count=0`.
5. If the above condition is satisfied then run a loop until present[i] comes to be false. Inside the loop increment `count` and `i`.
6. Once the loop ends store max count in `maxcount` variable.

#### Java

```Java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashMap<Integer, Boolean> present=new HashMap<>();
        HashMap<Integer, Boolean> checked=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            present.put(nums[i],true);
        }
        int ans=0;
        for(int i=0;i<nums.length;i++){
           if(!checked.containsKey(nums[i]) && !present.getOrDefault(nums[i]-1, false)){
            int curr_len=0;
            int start=nums[i];
            while(present.getOrDefault(start,false)){
                curr_len+=1;
                checked.put(start,true);
                start++;
            }
            ans=Math.max(curr_len,ans);

           }
                   }
                   return ans;
    }
}


```

#### Python

```python

class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        present={}
        checked={}
        maxcount=0
        for num in nums:
            present[num]=True
        for num in nums:

            while(not present.get(num-1,False) and  not checked.get(num,False)):
                count=0
                i=num
                while(present.get(i,False)):
                    checked[i]=True
                    i+=1
                    count+=1

                maxcount=max(count,maxcount)
        return maxcount

```

Time Complexity: O(n)
Space Complexity O(n)

---

**Materials To Read/Watch**

1. [Read best blog here](https://takeuforward.org/data-structure/longest-consecutive-sequence-in-an-array/)
