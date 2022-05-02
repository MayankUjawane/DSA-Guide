# Wildcard Matching
Question -> [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)    

### Recursion
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        return isMatch(m-1, s, n-1, p);
    }
    private boolean isMatch(int i, String s, int j, String p) {
        if(i<0 && j<0) return true;
        if(i>=0 && j<0) return false;
        if(i<0 && j>=0) {
            for(int index=0; index<=j; index++) {
                if(p.charAt(index) != '*') return false;
            }
            return true;
        }
        
        if((s.charAt(i) == p.charAt(j)) || (p.charAt(j) == '?')) {
            return isMatch(i-1, s, j-1, p);
        } else if(p.charAt(j) == '*') {
            boolean consider = isMatch(i, s, j-1, p); 
            boolean notConsider = isMatch(i-1, s, j, p); // considering * as empty character
            return (consider || notConsider);
        } else {
            return false;
        }
    }
}
```           
> `Time Complexity` : **Exponential**             
> `Space Complexity` : **O(M+N)**    
---
### Memoization
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        int[][] dp = new int[m][n];
        return isMatch(m-1, s, n-1, p, dp);
    }
    private boolean isMatch(int i, String s, int j, String p, int[][] dp) {
        if(i<0 && j<0) return true;
        if(i>=0 && j<0) return false;
        if(i<0 && j>=0) {
            for(int index=0; index<=j; index++) {
                if(p.charAt(index) != '*') return false;
            }
            return true;
        }
        
        if(dp[i][j] != 0) return (dp[i][j] == 1) ? true : false;
        
        boolean ans = false;
        if((s.charAt(i) == p.charAt(j)) || (p.charAt(j) == '?')) {
            ans = isMatch(i-1, s, j-1, p, dp);
        } else if(p.charAt(j) == '*') {
            boolean consider = isMatch(i, s, j-1, p, dp); 
            boolean notConsider = isMatch(i-1, s, j, p, dp); // considering * as empty character
            ans = (consider || notConsider);
        }
        
        if(ans == false) {
            dp[i][j] = 2;
        } else {
            dp[i][j] = 1;
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Memoization with Index Shifting
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        int[][] dp = new int[m+1][n+1];
        return isMatch(m, s, n, p, dp);
    }
    private boolean isMatch(int i, String s, int j, String p, int[][] dp) {
        if(i==0 && j==0) return true;
        if(i>0 && j==0) return false;
        if(i==0 && j>0) {
            for(int index=0; index<j; index++) {
                if(p.charAt(index) != '*') return false;
            }
            return true;
        }
        
        if(dp[i][j] != 0) return (dp[i][j] == 1) ? true : false;
        
        boolean ans = false;
        if((s.charAt(i-1) == p.charAt(j-1)) || (p.charAt(j-1) == '?')) {
            ans = isMatch(i-1, s, j-1, p, dp);
        } else if(p.charAt(j-1) == '*') {
            boolean consider = isMatch(i, s, j-1, p, dp); 
            boolean notConsider = isMatch(i-1, s, j, p, dp); // considering * as empty character
            ans = (consider || notConsider);
        }
        
        if(ans == false) {
            dp[i][j] = 2;
        } else {
            dp[i][j] = 1;
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m+1][n+1];
        // base case
        dp[0][0] = true;
        for(int i=1; i<=m; i++) dp[i][0] = false;
        for(int j=1; j<=n; j++) {
            if(p.charAt(j-1) == '*') {
                dp[0][j] = true;
            } else {
                break;
            }
        }
        
        for(int i=1; i<=m; i++) {
            for(int j=1; j<=n; j++) {
                boolean ans = false;
                if((s.charAt(i-1) == p.charAt(j-1)) || (p.charAt(j-1) == '?')) {
                    ans = dp[i-1][j-1];
                } else if(p.charAt(j-1) == '*') {
                    boolean consider = dp[i][j-1]; 
                    boolean notConsider = dp[i-1][j]; // considering * as empty character
                    ans = (consider || notConsider);
                }
                dp[i][j] = ans;
            }
        }
        return dp[m][n];
    }
}
```
> `Time Complexity` : **O(M\*N)**             
> `Space Complexity` : **O(M\*N)** 
---
### Tabulation with Space Optimization
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[] prev = new boolean[n+1];
        // base case
        prev[0] = true;
        for(int j=1; j<=n; j++) {
            if(p.charAt(j-1) == '*') {
                prev[j] = true;
            } else {
                break;
            }
        }
        
        for(int i=1; i<=m; i++) {
            boolean[] curr = new boolean[n+1];
            curr[0] = false;
            for(int j=1; j<=n; j++) {
                boolean ans = false;
                if((s.charAt(i-1) == p.charAt(j-1)) || (p.charAt(j-1) == '?')) {
                    ans = prev[j-1];
                } else if(p.charAt(j-1) == '*') {
                    boolean consider = curr[j-1]; 
                    boolean notConsider = prev[j]; // considering * as empty character
                    ans = (consider || notConsider);
                }
                curr[j] = ans;
            }
            prev = curr;
        }
        return prev[n];
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
Video Explanations -> [Wildcard Matching](https://youtu.be/ZmlQ3vgAOMo?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
