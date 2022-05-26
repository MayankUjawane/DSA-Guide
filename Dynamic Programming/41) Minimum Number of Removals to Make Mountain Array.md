# Minimum Number of Removals to Make Mountain Array
Question -> [Minimum Number of Removals to Make Mountain Array](https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array/)       

### Tabulation
```java
class Solution {
    public int minimumMountainRemovals(int[] nums) {
        int n = nums.length;
        //step:1 find the longest increasing subsequences till i
        int[] leftLis = lisFromLeft(nums, n);
        //step : 2 find longest decreasing subsequence starting from i
        int[] rightLis = lisFromRight(nums, n);
        
        // step 3: now find longest bitonic subsequence, but ensure that there something on the left and right 
        // of a particular index i inorder to make it a mountain which means leftLis[i] > 1 and rightLis[i] > 1
        int max = 0;
        for(int i=0; i<n; i++) {
            // For this type of test cases [9,8,1,7,6,5,4,3,2,1]
            if(leftLis[i]==1 || rightLis[i]==1) continue;
            int length = leftLis[i]+rightLis[i]-1;
            if(max<length) max = length;
        }
        
        //step 4: min remove is size of the original array - the length of the longest bitonic subsequence found
        return n-max;
    }
    private static int[] lisFromLeft(int[] arr, int n) {
        int[] dp = new int[n];
        for(int i=0; i<n; i++) {
            dp[i] = 1;
            for(int j=0; j<i; j++) {
                if(arr[i]>arr[j] && dp[i]<dp[j]+1) {
                    dp[i] = dp[j] + 1;
                }
            }
        }
        return dp;
    }
    private static int[] lisFromRight(int[] arr, int n) {
        int[] dp = new int[n];
        for(int i=n-1; i>=0; i--) {
            dp[i] = 1;
            for(int j=n-1; j>i; j--) {
                if(arr[i]>arr[j] && dp[i]<dp[j]+1) {
                    dp[i] = dp[j] + 1;
                }
            }
        }
        return dp;
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Minimum Number of Removals to Make Mountain Array](https://youtu.be/y4vN0WNdrlg?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
