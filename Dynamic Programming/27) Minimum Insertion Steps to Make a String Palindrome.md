# Minimum Insertion Steps to Make a String Palindrome
Question -> [Minimum Insertion Steps to Make a String Palindrome](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/)   

### Tabulation
```java
class Solution {
    public int minInsertions(String s) {
        int lps = largestPalindromicSubsequence(s);
        int n = s.length();
        return n-lps;
    }
    private int largestPalindromicSubsequence(String s) {
        StringBuilder sb = new StringBuilder(s);
        String rev = sb.reverse().toString();
        return largestCommonSubsequence(s, rev);
    }
    private int largestCommonSubsequence(String s, String t) {
        int n = s.length();
        int[][] dp = new int[n+1][n+1];
        // base case 
        for(int i=0; i<=n; i++) {
            dp[0][i] = 0;
            dp[i][0] = 0;
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
Video Explanation -> [Minimum Insertion Steps to Make a String Palindrome](https://youtu.be/xPBLEj41rFU?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
