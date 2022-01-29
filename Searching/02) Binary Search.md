# Binary Search 
> Binary Search is a searching algorithm that finds the position of a target value within a **sorted array**. 
> ### Algorithm
> * Compare x with the middle element.
> * If x matches with the middle element, return the mid index.
> * Else If x is greater than the mid element, then x can only lie in the right half subarray after the mid element. So shift start to mid+1.
> * Else (x is smaller) then search in the left half. So shift end to mid-1.
### Implementation
```java
public class Solution{
    public int binarySearch(int[] arr, int num) {
        int start = 0;
        int end = arr.length-1;
        while(start <= end) {
            int mid = (start+end)/2;
            if(arr[mid] > num) {
                end = mid-1;
            } else if (arr[mid] < num) {
                start = mid+1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}
```
> `Time Complexity` : **O(log n)**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Binary Search](https://youtu.be/j6BgMBIOCLQ?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>
