# Longest Common Substring 
Question -> [Longest Common Substring](https://www.codingninjas.com/codestudio/problems/longest-common-substring_1235207)    

### Recursion
```java
public class Solution {
    public static int lcs(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        return lcs(m, s1, n, s2, 0);
    }
    public static int lcs(int index1, String s1, int index2, String s2, int lcsCount) {
        if(index1 == 0 || index2 == 0) return lcsCount;

        int length1 = lcsCount;
        if(s1.charAt(index1-1) == s2.charAt(index2-1)) {
            length1 = lcs(index1-1, s1, index2-1, s2, lcsCount+1);
        }
        int length2 = lcs(index1-1, s1, index2, s2, 0);
        int length3 = lcs(index1, s1, index2-1, s2, 0);

        return Math.max(length1, Math.max(length2,length3));
    }
}
```           
> `Time Complexity` : **O(3<sup>(M+N)</sup>)**, where M = Length of string1 and N = Length of string2          
> `Space Complexity` : **O(M+N)**    
---
### Memoization with Index Shifting
```java
import java.util.*;
public class Solution {
    public static int lcs(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        int maxLcsCount = Math.min(m,n);
        int[][][] dp = new int[m+1][n+1][maxLcsCount+1];
        for(int[][] arr : dp) {
            for(int[] row : arr) Arrays.fill(row,-1);
        }	
        return lcs(m, s1, n, s2, 0, dp);
    }
    public static int lcs(int index1, String s1, int index2, String s2, int lcsCount, int[][][] dp) {
        if(index1 == 0 || index2 == 0) return lcsCount;

        if(dp[index1][index2][lcsCount] != -1) return dp[index1][index2][lcsCount];

        int length1 = lcsCount;
        if(s1.charAt(index1-1) == s2.charAt(index2-1)) {
            length1 = lcs(index1-1, s1, index2-1, s2, lcsCount+1, dp);
        }
        int length2 = lcs(index1-1, s1, index2, s2, 0, dp);
        int length3 = lcs(index1, s1, index2-1, s2, 0, dp);

        return dp[index1][index2][lcsCount] = Math.max(length1, Math.max(length2,length3));
    }
}
```
> `Time Complexity` : **O(M\*N\*N)**            
> `Space Complexity` : **O(M+N)+O(M\*N\*N)**, for Recursion Stack and dp array
---
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
