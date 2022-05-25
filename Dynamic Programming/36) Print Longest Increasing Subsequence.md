# Print Longest Increasing Subsequence

```java
class Solution {
    public void printLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        int[] hash = new int[n];
        
        int maxLength = 1;
        dp[0] = 1;
        hash[0] = 0;
        int lastElementOfLis = 0;
        
        for(int i=1; i<n; i++) {
            hash[i] = i;
            dp[i] = 1;
            for(int j=0; j<i; j++) {
                if(nums[i]>nums[j] && dp[i]<dp[j]+1) {
                    dp[i] = dp[j]+1;
                    hash[i] = j;
                }
            }
            if(maxLength < dp[i]) {
                maxLength = dp[i];
                lastElementOfLis = i;
            }
        }
        
        int[] lis = new int[maxLength];
        lis[maxLength-1] = nums[lastElementOfLis];
        int index = maxLength-2;
        while(hash[lastElementOfLis] != lastElementOfLis) {
            lastElementOfLis = hash[lastElementOfLis];
            lis[index--] = nums[lastElementOfLis];
        }
        
        System.out.println(Arrays.toString(lis));
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Print Longest Increasing Subsequence](https://youtu.be/IFfYfonAFGc?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)  
<hr>
