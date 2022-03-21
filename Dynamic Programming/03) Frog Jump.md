# Frog Jump
Question -> [Frog Jump](https://www.codingninjas.com/codestudio/problems/frog-jump_3621012)    

### Recursion
```java
class Solution {
    public static int frogJump(int n, int heights[]) {
        return jump(n-1, heights);
    }
    public static int jump(int n, int[] heights) {
        if(n == 0) return 0;
        int oneStep = jump(n-1, heights) + Math.abs(heights[n]-heights[n-1]);
        int twoStep = Integer.MAX_VALUE;
        if(n > 1) {
            twoStep = jump(n-2, heights) + Math.abs(heights[n]-heights[n-2]);
        }
        return Math.min(oneStep, twoStep);
    }
}
```
> `Recurrence Relation` : **T(n) = T(n-1)+T(n-2)+c**         
> `Time Complexity` : **O(2<sup>N</sup>)**          
> `Space Complexity` : **O(N)**
---
### Memorization
```java
class Solution {
    public static int frogJump(int n, int heights[]) {
        int[] dp = new int[n];
        return frogJump(n-1, heights, dp);
    }
    public static int frogJump(int n, int[] heights, int[] dp) {
        if(n == 0) return 0;
        if(dp[n] != 0) return dp[n]; 
        int oneStep = frogJump(n-1, heights, dp) + Math.abs(heights[n]-heights[n-1]);
        int twoStep = Integer.MAX_VALUE;
        if(n > 1) {
            twoStep = frogJump(n-2, heights, dp) + Math.abs(heights[n]-heights[n-2]);
        }   
        dp[n] = Math.min(oneStep, twoStep);
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
    public static int frogJump(int n, int heights[]) {
        int[] dp = new int[n];
        dp[0] = 0;
        for(int i=1; i<n; i++) {
            int oneStep = dp[i-1] + Math.abs(heights[i]-heights[i-1]);
            int twoStep = Integer.MAX_VALUE;
            if(i > 1) {
                twoStep = dp[i-2] + Math.abs(heights[i]-heights[i-2]);
            }   
            dp[i] = Math.min(oneStep, twoStep); 
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
    public static int frogJump(int n, int heights[]) {
        int prev1 = 0, prev2 = 0;
        for(int i=1; i<n; i++) {
            int oneStep = prev1 + Math.abs(heights[i]-heights[i-1]);
            int twoStep = Integer.MAX_VALUE;
            if(i > 1) {
                twoStep = prev2 + Math.abs(heights[i]-heights[i-2]);
            }   
            int curr = Math.min(oneStep, twoStep); 
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
Video Explanations -> [Frog Jump](https://youtu.be/EgG3jsGoPvQ?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
