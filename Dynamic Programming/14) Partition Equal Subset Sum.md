# Partition Equal Subset Sum
Question -> [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)    

### Recursion
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int n = nums.length;
        if(n == 1) return false;
        
        int totalSum = 0;
        for(int num : nums) totalSum += num;
        if(totalSum % 2 != 0) return false;
        
        int target = totalSum/2;
        return subsetSum(n-1, target, nums);
    }
    public static boolean subsetSum(int index, int target, int[] arr) {
        if(target < 0) return false;
        if(target == 0) return true;
        if(index == 0) return (arr[index] == target);
        
        boolean take = subsetSum(index-1, target-arr[index], arr);
        boolean notTake = subsetSum(index-1, target, arr);
        return (take || notTake);
    }
}
```         
> `Recurrence Realtion` : **T(N) = 2(T(N-1))+C**     
> `Time Complexity` : **O(2<sup>(N)</sup>)+O(N)**          
> `Space Complexity` : **O(N)**    
---
### Memoization
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int n = nums.length;
        if(n == 1) return false;
        
        int totalSum = 0;
        for(int num : nums) totalSum += num;
        if(totalSum % 2 != 0) return false;
        
        int target = totalSum/2;
        int[][] dp = new int[n][target+1];
        return subsetSum(n-1, target, nums, dp);
    }
    public static boolean subsetSum(int index, int target, int[] arr, int[][] dp) {
        if(target < 0) return false;
        if(target == 0) return true;
        if(index == 0) return (arr[index] == target);
        
        if(dp[index][target] != 0) return (dp[index][target] == 1);
        boolean take = subsetSum(index-1, target-arr[index], arr, dp);
        boolean notTake = subsetSum(index-1, target, arr, dp);
        
        boolean ans = (take || notTake);
        dp[index][target] = (ans==true) ? 1 : 2;
        return ans;
    }
}
```
> `Time Complexity` : **O(N\*K)+O(N)**, K = target          
> `Space Complexity` : **O(N)+O(N\*K)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int n = nums.length;
        if(n == 1) return false;
        
        int totalSum = 0;
        for(int num : nums) totalSum += num;
        if(totalSum % 2 != 0) return false;
        
        int target = totalSum/2;
        return subsetSum(n-1, target, nums);
    }
    public static boolean subsetSum(int n, int k, int[] arr) {
        boolean[][] dp = new boolean[n][k+1];
        // base case
        // for target = 0 at any index
        for(int index=0; index<n; index++) {
            dp[index][0] = true;
        }
        // when at index=0, target is equal to arr[0]
        if(arr[0] <= k) dp[0][arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            for(int target=1; target<=k; target++) {
                boolean taken = false;
                if(target >= arr[index]) {
                    taken = dp[index-1][target-arr[index]];
                }
                boolean notTaken = dp[index-1][target];
                dp[index][target] = (taken || notTaken);
            }
        }
        return dp[n-1][k];
    }
}
```
> `Time Complexity` : **O(N\*K)+O(N)**          
> `Space Complexity` : **O(N\*K)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int n = nums.length;
        if(n == 1) return false;
        
        int totalSum = 0;
        for(int num : nums) totalSum += num;
        
        if(totalSum % 2 != 0) return false;
        
        int target = totalSum/2;
        return subsetSum(n-1, target, nums);
    }
    public static boolean subsetSum(int n, int k, int[] arr) {
        boolean[] prev = new boolean[k+1];
        // for target = 0 at any index
        prev[0] = true;
        // when at index=0, target is equal to arr[0]
        if(arr[0] <= k) prev[arr[0]] = true;
        
        for(int index=1; index<n; index++) {
            boolean[] curr = new boolean[k+1];
            curr[0] = true;
            for(int target=1; target<=k; target++) {
                boolean taken = false;
                if(target >= arr[index]) {
                    taken = prev[target-arr[index]];
                }
                boolean notTaken = prev[target];
                curr[target] = (taken || notTaken);
            }
            prev = curr;
        }
        return prev[k];
    }
}
```
> `Time Complexity` : **O(N\*K)+O(N)**          
> `Space Complexity` : **O(K)+O(K)**, for prev and curr arrays.
---
Video Explanations -> [Partition Equal Subset Sum](https://youtu.be/7win3dcgo3k?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
