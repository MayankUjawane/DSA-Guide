# Minimum Cost to Cut a Stick
Question -> [Minimum Cost to Cut a Stick](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/)    

### Recursion
```java
class Solution {
    public int minCost(int n, int[] cuts) {
        Arrays.sort(cuts);
        int l = cuts.length;
        return func(0, l-1, l, cuts, n);
    }
    private int func(int i, int j, int l, int[] cuts, int n) {
        if(i>j) return 0;
        
        int cost = 0;
        cost += (j==l-1) ? n : cuts[j+1];
        cost -= (i==0) ? 0 : cuts[i-1];
        
        int min = Integer.MAX_VALUE;
        for(int index=i; index<=j; index++) {
            int val = func(i, index-1, l, cuts, n) + func(index+1, j, l, cuts, n);
            min = Math.min(min,val);
        }
        
        cost += min;
        return cost;
    }
}
```           
> `Time Complexity` : **Exponential**    
> `Space Complexity` : **O(N)**, N=cuts.length 
---
### Memoization
```java
class Solution {
    public int minCost(int n, int[] cuts) {
        Arrays.sort(cuts);
        int l = cuts.length;
        int[][] dp = new int[l][l];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return func(0, l-1, l, cuts, n, dp);
    }
    private int func(int i, int j, int l, int[] cuts, int n, int[][] dp) {
        if(i>j) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        int cost = 0;
        cost += (j==l-1) ? n : cuts[j+1];
        cost -= (i==0) ? 0 : cuts[i-1];
        
        int min = Integer.MAX_VALUE;
        for(int index=i; index<=j; index++) {
            int val = func(i, index-1, l, cuts, n, dp) + func(index+1, j, l, cuts, n, dp);
            min = Math.min(min,val);
        }
        
        cost += min;
        return dp[i][j] = cost;
    }
}
```
> `Time Complexity` : **O(N<sup>3</sup>)**, N = cuts.length           
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int minCost(int n, int[] cuts) {
        Arrays.sort(cuts);
        int l = cuts.length;
        int[][] dp = new int[l][l];
        
        for(int i=l-1; i>=0; i--) {
            for(int j=0; j<l; j++) {
                if(i>j) continue;
                int cost = 0;
                cost += (j==l-1) ? n : cuts[j+1];
                cost -= (i==0) ? 0 : cuts[i-1];
                
                int min = Integer.MAX_VALUE;
                for(int index=i; index<=j; index++) {
                    int val = 0;
                    if(index-1 >= 0) val += dp[i][index-1];
                    if(index+1 < l) val += dp[index+1][j];
                    min = Math.min(min,val);
                }
                dp[i][j] = cost + min;
            }
        }
        
        return dp[0][l-1];
    }
}
```
> `Time Complexity` : **O(N<sup>3</sup>)**             
> `Space Complexity` : **O(N\*N)** 
---
Video Explanations -> [Minimum Cost to Cut a Stick](https://youtu.be/xwomavsC86c?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
