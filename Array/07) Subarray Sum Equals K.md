# Subarray Sum Equals K
> Question -> [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)    

### Implementation
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum=0, count=0;
        Map<Integer,Integer> map = new HashMap();
        map.put(0,1);
        
        for(int num: nums) {
            sum += num;
            if(map.containsKey(sum-k)) {
                count += map.get(sum-k);
            }
            map.put(sum, map.getOrDefault(sum,0)+1);
        }
        
        return count;
    }
}
```
> `Time Complexity` : **O(N)**                   
> `Space Complexity` : **O(N)**
---
