# Longest String Chain
Question -> [Longest String Chain](https://leetcode.com/problems/longest-string-chain/)       

### Tabulation
```java
class Solution {
    public int longestStrChain(String[] words) {
        Arrays.sort(words, (x,y)->x.length()-y.length());
        int n = words.length;
        int[] dp = new int[n];
        int max=0;
        for(int i=0; i<n; i++) {
            dp[i] = 1; 
            for(int j=0; j<i; j++) {
                if(isPossible(words[i],words[j]) && dp[i]<dp[j]+1) {
                    dp[i] = dp[j]+1;
                }
            }
            max = Math.max(max,dp[i]);
        }
        return max;
    }
    // T.C.-> O(Length of String)
    private boolean isPossible(String s, String t) {
        int l1=s.length(), l2=t.length();
        if(l1 != l2+1) return false;
        
        int first=0, second=0;
        while(first<l1 && second<l2) {
            if(s.charAt(first)==t.charAt(second)) {
                first++;
                second++;
            } else {
                first++;
            }
        }
        return (second==l2);
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Longest String Chain](https://youtu.be/YY8iBaYcc4g?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
