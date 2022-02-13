# Subsets
> Question -> [Subsets](https://leetcode.com/problems/subsets/)    

### Implementation
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList();
        int n = nums.length;
        int total = (int)Math.pow(2,n);
        
        for(int i=0; i<total; i++) {
            List<Integer> list = new ArrayList();
            int temp = i;
            for(int j=0; j<n; j++) {
                int r = temp%2;
                temp = temp/2;
                if(r == 1) list.add(nums[j]);
            }
            ans.add(list);
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(N\*(2<sup>N</sup>))**, outer loop is running for 2<sup>N</sup> times and inner loop is running for N times.                 
> `Space Complexity` : **O(N\*(2<sup>N</sup>))**, ans list will be of size 2<sup>N</sup> and the subsets can be maximum of length N, since each of N elements could be present or absent.
---
