# Number of Zero-Filled Subarrays
> Question -> [Number of Zero-Filled Subarrays](https://leetcode.com/problems/number-of-zero-filled-subarrays/)    

### Implementation
```java
class Solution {
    public long zeroFilledSubarray(int[] nums) {
        long ans = 0;
        int n = nums.length;
        
        int start = -1, curr = 0;
        
        while(curr<n) {
            int val = nums[curr];
            if(val==0) {
                start = curr;
            } else {
                curr++;
                continue;
            }
            
            while(curr<n && nums[curr] == 0) curr++;
            long diff = curr-start;
            // number of subarrays of length n = n*(n+1)/2
            long answer = diff*(diff+1)/2;
            ans += answer;
        }
        
        return ans;
    }
}
```
> `Time Complexity` : **O(N)**                   
> `Space Complexity` : **O(1)**
---
