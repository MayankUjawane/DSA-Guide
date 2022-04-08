# Longest Common Substring 
Question -> [Longest Common Substring](https://www.codingninjas.com/codestudio/problems/longest-common-substring_1235207)    

### Tabulation
```java
public class Solution {
    public static int lcs(String str1, String str2) {
        int m = str1.length();
        int n = str2.length();
        // using index shifting
        int[][] dp = new int[m+1][n+1];
        // base case 
        for(int i=0; i<=n; i++) dp[0][i] = 0;
        for(int i=0; i<=m; i++) dp[i][0] = 0;

        int ans = 0;
        for(int ind1=1; ind1<=m; ind1++) {
            for(int ind2=1; ind2<=n; ind2++) {
                if(str1.charAt(ind1-1) == str2.charAt(ind2-1)) {
                    dp[ind1][ind2] = 1 + dp[ind1-1][ind2-1];
                    ans = Math.max(ans,dp[ind1][ind2]);
                } else {
                    dp[ind1][ind2] = 0;
                }
            }
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M\*N)**
---
Video Explanations -> [Longest Common Substring](https://youtu.be/_wP9mWNPL5w?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
