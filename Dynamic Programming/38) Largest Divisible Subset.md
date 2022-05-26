# Largest Divisible Subset
Question -> [Largest Divisible Subset](https://leetcode.com/problems/largest-divisible-subset/)       

### Tabulation
```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int[] dp = new int[n];
        int[] prev = new int[n];
        int maxLength=0, lastIndex=-1;
        
        for(int i=0; i<n; i++) {
            dp[i] = 1;
            prev[i] = -1;
            int curr = nums[i];
            
            for(int j=0; j<i; j++) {
                if(curr%nums[j] == 0 && dp[j]+1 > dp[i]) {
                    dp[i] = dp[j]+1;
                    prev[i] = j;
                }
            }
            if(maxLength<dp[i]) {
                maxLength = dp[i];
                lastIndex = i;
            }
        }
        
        List<Integer> ans = new LinkedList();
        while(lastIndex != -1) {
            ans.add(0,nums[lastIndex]);
            lastIndex = prev[lastIndex];
        }
        
        return ans;
    }
}
```
> `Time Complexity` : **O(N\*N)**           
> `Space Complexity` : **O(N)**, for dp array
---
Video Explanations -> [Largest Divisible Subset](https://youtu.be/gDuZwBW9VvM?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
