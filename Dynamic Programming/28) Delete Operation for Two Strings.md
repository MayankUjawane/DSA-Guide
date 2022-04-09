# Delete Operation for Two Strings
Question -> [Delete Operation for Two Strings](https://leetcode.com/problems/delete-operation-for-two-strings/)   

### Tabulation
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int n = word1.length();
        int m = word2.length();
        int lcs = largestCommonSubsequence(word1, word2, n, m);
        return (n-lcs+m-lcs);
    }
    private int largestCommonSubsequence(String s, String t, int n, int m) {
        int[][] dp = new int[n+1][m+1];
        // base case
        for(int i=0; i<=n; i++) dp[i][0] = 0;
        for(int i=0; i<=m; i++) dp[0][i] = 0;
        
        for(int i=1; i<=n; i++) {
            for(int j=1; j<=m; j++) {
                if(s.charAt(i-1) == t.charAt(j-1)) {
                    dp[i][j] = 1 + dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return dp[n][m];
    }
}
```
> `Time Complexity` : **O(N\*M)**            
> `Space Complexity` : **O(N\*M)**
---
Video Explanation -> [Delete Operation for Two Strings](https://youtu.be/yMnH0jrir0Q?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
