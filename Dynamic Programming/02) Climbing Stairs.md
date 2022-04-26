# Climbing Stairs
Question -> [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)    

### Recursion
```java
class Solution {
    public int climbStairs(int n) {
        if(n < 0) return 0;
        if(n == 0) return 1;
        return (climbStairs(n-1) + climbStairs(n-2));
    }
}
```
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memoization
```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n+1];
        return climbStairs(n, dp);
    }
    public int climbStairs(int n, int[] dp) {
        if(n < 0) return 0;
        if(n == 0) return 1;
        if(dp[n] != 0) return dp[n];
        dp[n] = climbStairs(n-1, dp) + climbStairs(n-2, dp);
        return dp[n];
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)+O(N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int climbStairs(int n) {
        if(n < 2) return 1;
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2; i<=n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int climbStairs(int n) {
        if(n < 2) return 1;
        int oneStepBack = 1, twoStepBack = 1;
        for(int i=2; i<=n; i++) {
            int current = oneStepBack + twoStepBack;
            twoStepBack = oneStepBack;
            oneStepBack = current;
        }
        return oneStepBack;
    }
}
```
> `Time Complexity` : **O(N)**          
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Climbing Stairs](https://youtu.be/mLfjzJsN8us?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
