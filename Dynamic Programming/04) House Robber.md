# House Robber
Question -> [House Robber](https://leetcode.com/problems/house-robber/)    

### Recursion
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        return rob(nums, n-1);
    }
    public int rob(int[] nums, int index) {
        if(index == 0) return nums[0];
        if(index < 0) return 0;
        
        int pick = nums[index] + rob(nums, index-2);
        int notPick = rob(nums, index-1);
        return Math.max(pick, notPick);
    }
}
```
> `Recurrence Relation` : **T(n) = T(n-2)+T(n-1)+C**           
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memorization
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, -1);
        
        return rob(nums, n-1, dp);
    }
    public int rob(int[] nums, int index, int[] dp) {
        if(index < 0) return 0;
        if(index == 0) return nums[0];
        
        if(dp[index] != -1) return dp[index];
        
        int pick = nums[index] + rob(nums, index-2, dp);
        int notPick = rob(nums, index-1, dp);
        
        return dp[index] = Math.max(pick,notPick);
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)+O(N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = nums[0];
        for(int i=1; i<n; i++) {
            int pick = nums[i];
            if(i-2 >=0) pick += dp[i-2];
            int notPick = dp[i-1];
            dp[i] = Math.max(pick,notPick);
        }
        return dp[n-1];
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        int prev1 = nums[0], prev2 = -1; 
        for(int i=1; i<n; i++) {
            int pick = nums[i];
            if(prev2 >=0) pick += prev2;
            int notPick = prev1;
            
            int curr = Math.max(pick,notPick);
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(1)**
---
Video Explanations -> [House Robber](https://youtu.be/GrMBfJNk_NY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
