# Count Occurrences in Sorted Array

[Detailed indepth explanation](https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/)

Given a sorted array Arr of size N and a number X, you need to find the number of occurrences of X in Arr.

[Problem Link](https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number-of-occurrence)

```

Example 1:
Input:
 N = 7,  X = 3 , array[] = {2, 2 , 3 , 3 , 3 , 3 , 4}
Output: 4
Explanation:
 3 is occurring 4 times in
the given array so it is our answer.

Example 2:
Input:
 N = 8,  X = 2 , array[] = {1, 1, 2, 2, 2, 2, 2, 3}
Output: 5
Explanation:
 2 is occurring 5 times in the given array so it is our answer.


```

---

## **Approach**:

## **Solution**:

### **Brute Force**:

The approach is simple. We will linearly search the entire array, and try to increase the counter whenever we get the target value in the array. Using a for loop that runs from 0 to n - 1, containing an if the condition that checks whether the value at that index equals target. If true then increase the counter, at last return the counter.

### Java

```Java

import java.util.*;

public class Solution {
    public static int count(int arr[], int n, int x) {
        int cnt = 0;
        for (int i = 0; i < n; i++) {

            // counting the occurrences:
            if (arr[i] == x) cnt++;
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr =  {2, 4, 6, 8, 8, 8, 11, 13};
        int n = 8, x = 8;
        int ans = count(arr, n, x);
        System.out.println("The number of occurrences is: " + ans);
    }
}



```

Time Complexity: O(n)

Space Complexity O(1)

---

### **Best Approach**

Total number of occurrences = last occurrence - first occurrence + 1

#### Java

```Java

//{ Driver Code Starts
//Initial Template for Java



import java.util.*;
import java.io.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int tc = Integer.parseInt(br.readLine().trim());
        while (tc-- > 0) {
            String[] inputLine;
            inputLine = br.readLine().trim().split(" ");
            int n = Integer.parseInt(inputLine[0]);
            int x = Integer.parseInt(inputLine[1]);
            int[] arr = new int[n];
            inputLine = br.readLine().trim().split(" ");
            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(inputLine[i]);
            }

            int ans = new Solution().count(arr, n, x);
            System.out.println(ans);
        }
    }
}

// } Driver Code Ends


//User function Template for Java



class Solution {
    int count(int[] arr, int n, int x) {
        // code here
        int fo=-1;
        int lo=-1;
        int low=0;
        int high=n-1;
        while(low<=high){
            int mid=(low+high)/2;
            if(arr[mid]==x){
                fo=mid;
                high=mid-1;
            }
            else if (arr[mid]<x){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        if (fo==-1){
            return 0;
        }
        low=0;
        high=n-1;
        while(low<=high){
            int mid=(low+high)/2;
            if(arr[mid]==x){
                lo=mid;
                low=mid+1;
            }
            else if (arr[mid]<x){
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }

        return lo-fo+1;
    }
}

```

#### Python

```python


```

Time Complexity: O(2\*logN), where N = size of the given array.
Reason: We are basically using the binary search algorithm twice.

Space Complexity O(1)

---

**Materials To Read/Watch**

1. [TUF explanation](https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/)
