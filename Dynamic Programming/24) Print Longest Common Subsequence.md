# Print Longest Common Subsequence   

### Recursion
```java
class Main {
    public static void main(String[] args) {
      printLongestCommonSubsequence("abcde","bdgek");
    }
    public static void printLongestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        System.out.println(lcs(m-1, text1, n-1, text2));
    }
    public static String lcs(int index1, String text1, int index2, String text2) {
        if(index1<0 || index2<0) return "";
        // when both strings have same characters at particular indexes then move to the next indexes of both strings
        if(text1.charAt(index1) == text2.charAt(index2)) return (lcs(index1-1, text1, index2-1, text2) + text1.charAt(index1));
        // when strings have different characters then give chance to both the strings to match with next indexes
        String first = lcs(index1-1, text1, index2, text2);
        String second = lcs(index1, text1, index2-1, text2);
        return (first.length() > second.length()) ? first : second; 
    }
}
```           
> `Time Complexity` : **Exponential**          
> `Space Complexity` : **O(M+N)**, M = Length of first string and N = Length of second string    
---
### Tabulation
```java
class Main {
    public static void main(String[] args) {
        printLongestCommonSubsequence("abcde","bdgek");
    }
    public static void printLongestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m+1][n+1];
        // base case
        int length = Math.max(m,n);
        for(int index=0; index<=length; index++) {
            if(index<=m) dp[index][0] = 0;
            if(index<=n) dp[0][index] = 0;
        }
        
        for(int i=1; i<=m; i++) {
            for(int j=1; j<=n; j++) {
                if(text1.charAt(i-1) == text2.charAt(j-1)) dp[i][j] = 1 + dp[i-1][j-1];
                else dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
            }
        }
        
        StringBuilder sb = new StringBuilder();
        int i=m, j=n;
        while(i>0 && j>0) {
            if(text1.charAt(i-1) == text2.charAt(j-1)) {
                sb.insert(0, text2.charAt(j-1));
                i--;
                j--;
            } else {
                if(dp[i-1][j] > dp[i][j-1]) {
                    i--;
                } else {
                    j--;
                }
            }
        }
        System.out.println(sb.toString());
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M\*N)**
---
Video Explanations -> [Print Longest Common Subsequence](https://youtu.be/-zI4mrF2Pb4?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
