# Number of Longest Increasing Subsequence
Question -> [Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)       

### Tabulation
```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        int[] count = new int[n];
        int maxLength=1;
        for(int i=0; i<n; i++) {
            dp[i] = 1;
            count[i] = 1;
            for(int j=0; j<i; j++) {
                if(nums[i]>nums[j] && dp[i]<=dp[j]+1) {
                    if(dp[i]<dp[j]+1) {
                        dp[i] = dp[j]+1;
                        count[i] = count[j];
                    } else {
                        count[i] += count[j];
                    }
                }
            }
            if(dp[i]>maxLength) {
                maxLength = dp[i];
            }
        }
        
        int ans = 0;
        for(int i=0; i<n; i++) {
            if(dp[i]==maxLength) {
                ans += count[i];
            }
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Number of Longest Increasing Subsequence](https://youtu.be/cKVl1TFdNXg?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
