# Maximum Subarray
> Question -> [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)    

### Kadane's Algorithm
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = nums[0];
        int curr = nums[0];
        int n = nums.length;
        
        for(int i=1; i<n; i++) {
            if(curr < 0) curr = 0;
            curr += nums[i];
            if(curr > max) max = curr;
        }
        
        return max;
    }
}
```
> `Time Complexity` : **O(N)**                   
> `Space Complexity` : **O(1)**
---
