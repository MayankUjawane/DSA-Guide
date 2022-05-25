# Longest Increasing Subsequence
Question -> [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)       

### Recursion
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        return lengthOfLIS(0, -1, n, nums);
    }
    private int lengthOfLIS(int index, int prevIndex, int n, int[] nums) {
        if(index == n) return 0;
        
        int notTake = lengthOfLIS(index+1, prevIndex, n, nums);
        int take = 0;
        if(prevIndex == -1 || nums[index]>nums[prevIndex]) {
            take = 1 + lengthOfLIS(index+1, index, n, nums);
        }
        return Math.max(take,notTake);
    }
}
```           
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memoization
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[][] dp = new int[n][n+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return lengthOfLIS(0, -1, n, nums, dp);
    }
    private int lengthOfLIS(int index, int prevIndex, int n, int[] nums, int[][] dp) {
        if(index == n) return 0;
        
        if(dp[index][prevIndex+1] != -1) return dp[index][prevIndex+1];
        
        int notTake = lengthOfLIS(index+1, prevIndex, n, nums, dp);
        int take = 0;
        if(prevIndex == -1 || nums[index]>nums[prevIndex]) {
            take = 1 + lengthOfLIS(index+1, index, n, nums, dp);
        }
        return dp[index][prevIndex+1] = Math.max(take,notTake);
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[][] dp = new int[n+1][n+1];
        // base case
        for(int i=0; i<=n; i++) dp[n][i] = 0;
        
        for(int index=n-1; index>=0; index--) {
            for(int prevIndex=index-1; prevIndex>=-1; prevIndex--) {
                int notTake = dp[index+1][prevIndex+1];
                int take = 0;
                if(prevIndex == -1 || nums[index]>nums[prevIndex]) take = 1 + dp[index+1][index+1];
                
                dp[index][prevIndex+1] = Math.max(take,notTake);
            }
        }
        
        return dp[0][0];
    }
}
```
> `Time Complexity` : **O(N\*N)**             
> `Space Complexity` : **O(N\*N)** 
---
### Tabulation with Space Optimization
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] front = new int[n+1];
        // base case
        for(int i=0; i<=n; i++) front[i] = 0;
        
        for(int index=n-1; index>=0; index--) {
            int[] curr = new int[n+1];
            for(int prevIndex=index-1; prevIndex>=-1; prevIndex--) {
                int notTake = front[prevIndex+1];
                int take = 0;
                if(prevIndex == -1 || nums[index]>nums[prevIndex]) take = 1 + front[index+1];
                
                curr[prevIndex+1] = Math.max(take,notTake);
            }
            front = curr;
        }
        
        return front[0];
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)+O(N)**, for front and curr arrays.
---
### Tabulation Method 2
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        
        int maxLength = 1;
        dp[0] = 1;
        for(int i=1; i<n; i++) {
            dp[i] = 1;
            for(int j=0; j<i; j++) {
                if(nums[i]>nums[j]) {
                    dp[i] = Math.max(dp[i],dp[j]+1);
                }
            }
            maxLength = Math.max(maxLength,dp[i]);
        }
        return maxLength;
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Longest Increasing Subsequence](https://youtu.be/ekcwMsSIzVc?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
