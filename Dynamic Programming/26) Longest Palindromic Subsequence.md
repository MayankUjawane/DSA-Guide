# Longest Palindromic Subsequence
Question -> [Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)   

> **Logic**    
> We will be finding the longest common subsequence between string s and reverse of string s and this will give us Longest Palindromic Subsequence.       

### Tabulation
```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        StringBuilder sb = new StringBuilder(s);
        String rev = sb.reverse().toString();
        return lcs(s, rev);
    }
    private int lcs(String s, String t) {
        int n = s.length();
        int[][] dp = new int[n+1][n+1];
        // base case 
        for(int i=0; i<=n; i++) {
            dp[i][0] = 0;
            dp[0][i] = 0;
        }
        for(int i=1; i<=n; i++) {
            for(int j=1; j<=n; j++) {
                if(s.charAt(i-1) == t.charAt(j-1)) {
                    dp[i][j] = 1 + dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return dp[n][n];
    }
}
```
> `Time Complexity` : **O(N\*N)**            
> `Space Complexity` : **O(N\*N)**
---
Video Explanations -> [Longest Palindromic Subsequence](https://youtu.be/6i_T5kkfv4A?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
