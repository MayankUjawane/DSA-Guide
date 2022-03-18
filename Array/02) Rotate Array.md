# Rotate Array
Question -> [Rotate Array](https://leetcode.com/problems/rotate-array/)    

### With Extra Space
```java
public class Solution{
    public void rotate(int[] nums, int k) {
        int length = nums.length;
        k = k % length;
        if(k == 0) return;
        
        int[] arr = new int[length];
        for(int i=0; i<length; i++) {
            arr[i] = nums[i];
        }
        for(int i=0; i<length; i++) {
            if(i<k) {
                nums[i] = arr[length-k+i];
            } else {
                nums[i] = arr[i-k];
            }
        }
    }
}
```
> `Time Complexity` : **O(n)**       
> `Space Complexity` : **O(n)**
---
### Without Extra Space
```java
public class Solution{
    public void rotate(int[] nums, int k) {
        int length = nums.length;
        k = k % length;
        if(k == 0) return;
        // Reverse all elements before last k elements
        reverse(nums, 0, length-1-k);
        // Reverse last k elements
        reverse(nums, length-k, length-1);
        // Reverse the entire array
        reverse(nums, 0, length-1);
    }
    
    public void reverse(int[] arr, int start, int end) {
        while(start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
}
```
> `Time Complexity` : **O(n)**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Rotate Array](https://youtu.be/8RErc0VXAo8?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>
