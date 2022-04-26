# House Robber II
Question -> [House Robber II](https://leetcode.com/problems/house-robber-ii/)    

### Recursion
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if(n == 1) return nums[0];
        int leavingFirst = rob(nums, n-1, 1);
        int leavingLast = rob(nums, n-2, 0);
        return Math.max(leavingFirst,leavingLast);
    }
    public int rob(int[] nums, int index, int last) {
        if(index == last) return nums[last];
        if(index < last) return 0;
        
        int pick = nums[index] + rob(nums, index-2, last);
        int notPick = rob(nums, index-1, last);
        return Math.max(pick, notPick);
    }
}
```
> `Recurrence Relation` : **T(n) = T(n-2)+T(n-1)+C**           
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memoization
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if(n == 1) return nums[0];
        int[] dp1 = new int[n];
        int[] dp2 = new int[n];
        for(int i=0; i<n; i++) {
            dp1[i] = -1;
            dp2[i] = -1;
        }
        int leavingFirst = rob(nums, n-1, 1, dp1);
        int leavingLast = rob(nums, n-2, 0, dp2);
        return Math.max(leavingFirst,leavingLast);
    }
    public int rob(int[] nums, int index, int last, int[] dp) {
        if(index == last) return nums[last];
        if(index < last) return 0;
        
        if(dp[index] != -1) return dp[index];
        int pick = nums[index] + rob(nums, index-2, last, dp);
        int notPick = rob(nums, index-1, last, dp);
        return dp[index] = Math.max(pick, notPick);
    }
}
```
> `Time Complexity` : **O(N)+O(N)**          
> `Space Complexity` : **O(N)+O(N)+O(N)**, for Recursion Stack and dp arrays
---
### Tabulation
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if(n == 1) return nums[0];
        int[] dp1 = new int[n];
        int[] dp2 = new int[n];
        for(int i=0; i<n; i++) {
            dp1[i] = -1;
            dp2[i] = -1;
        }
        int leavingFirst = rob(nums, 1, n-1, dp1);
        int leavingLast = rob(nums, 0, n-2, dp2);
        return Math.max(leavingFirst,leavingLast);
    }
    public int rob(int[] nums, int start, int last, int[] dp) {
        dp[start] = nums[start];
        for(int i=start+1; i<=last; i++) {
            int pick = nums[i];
            if(i-2 >= start) pick += dp[i-2];
            int notPick = dp[i-1];
            dp[i] = Math.max(pick,notPick);
        }
        return dp[last];
    }
}
```
> `Time Complexity` : **O(N)+O(N)**          
> `Space Complexity` : **O(N)+O(N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if(n == 1) return nums[0];
        int prev1, prev2;
        
        prev1 = nums[1];
        prev2 = -1;
        int leavingFirst = rob(nums, 1, n-1, prev1, prev2);
        
        prev1 = nums[0];
        prev2 = -1;
        int leavingLast = rob(nums, 0, n-2, prev1, prev2);
        
        return Math.max(leavingFirst,leavingLast);
    }
    public int rob(int[] nums, int start, int last, int prev1, int prev2) {
        for(int i=start+1; i<=last; i++) {
            int pick = nums[i];
            if(i-2 >= start) pick += prev2;
            int notPick = prev1;
            int curr = Math.max(pick,notPick);
            
            prev2 = prev1; 
            prev1 = curr;
        }
        return prev1;
    }
}
```
> `Time Complexity` : **O(N)+O(N)**          
> `Space Complexity` : **O(1)**
---
Video Explanations -> [House Robber II](https://youtu.be/3WaxQMELSkw?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
