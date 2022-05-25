# Longest Increasing Subsequence (Binary Search)
Question -> [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)       

### Using Binary Search
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] arr = new int[n];
        int maxLength = 0;
        
        for(int i=0; i<n; i++) {
            int curr = nums[i];
            int index = binarySearch(arr, 0, maxLength, curr);
            if(index==maxLength) maxLength++;
            arr[index] = nums[i];
        }
        
        return maxLength;
    }
    // binary search will return the upper bond index for target if target is not found
    private int binarySearch(int[] arr, int start, int end, int target) {
        while(start < end) {
            int mid = (start+end)/2;
            if(arr[mid] > target) {
                end = mid;
            } else if(arr[mid] < target) {
                start = mid+1;
            } else {
                return mid;
            }
        }
        return start;
    }
}
```
> `Time Complexity` : **O(NlogN)**           
> `Space Complexity` : **O(N)**
---
Video Explanations -> [Longest Increasing Subsequence](https://youtu.be/on2hvxBXJH4?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
