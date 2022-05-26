# Longest Bitonic Sequence
Question -> [Longest Bitonic Sequence](https://www.codingninjas.com/codestudio/problems/longest-bitonic-sequence_1062688)       

### Tabulation
```java
public class Solution {
    public static int longestBitonicSequence(int[] arr, int n) {
        int[] leftLis = lisFromLeft(arr,n);
        int[] rightLis = lisFromRight(arr,n);
        
        int max = 0;
        int[] bitonic = new int[n];
        for(int i=0; i<n; i++) {
            bitonic[i] = leftLis[i]+rightLis[i]-1;
            if(max<bitonic[i]) max = bitonic[i];
        }
        return max;
    }
    private static int[] lisFromLeft(int[] arr, int n) {
        int[] dp = new int[n];
        for(int i=0; i<n; i++) {
            dp[i] = 1;
            for(int j=0; j<i; j++) {
                if(arr[i]>arr[j] && dp[i]<dp[j]+1) {
                    dp[i] = dp[j] + 1;
                }
            }
        }
        return dp;
    }
    private static int[] lisFromRight(int[] arr, int n) {
        int[] dp = new int[n];
        for(int i=n-1; i>=0; i--) {
            dp[i] = 1;
            for(int j=n-1; j>i; j--) {
                if(arr[i]>arr[j] && dp[i]<dp[j]+1) {
                    dp[i] = dp[j] + 1;
                }
            }
        }
        return dp;
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Longest Bitonic Sequence](https://youtu.be/y4vN0WNdrlg?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
