# Subarray Product Less Than K
> Question -> [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)    

### Implementation
```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if(k<=1) return 0;
        int product = 1;
        int start = 0;
        int n = nums.length;
        int ans = 0;
        
        for(int curr=0; curr<n; curr++) {
            product *= nums[curr];
            while(product >= k) product /= nums[start++];
            ans += (curr-start+1);
        }
        
        return ans;
    }
}
```
> `Time Complexity` : **O(N)**                   
> `Space Complexity` : **O(1)**
---
