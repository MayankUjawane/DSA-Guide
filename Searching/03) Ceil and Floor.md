# Ceil and Floor
Question -> [Ceil and Floor](https://www.pepcoding.com/resources/online-java-foundation/function-and-arrays/ceil-floor-official/ojquestion)    

### Implementation
```java
public class Solution{
    public void printCeilAndFloor(int[] arr, int num) {
        int start = 0;
        int end = arr.length-1;
        int ceil = 0, floor = 0;
        while(start <= end) {
            int mid = (start+end)/2;
            if(arr[mid] > num) {
                ceil = arr[mid];
                end = mid-1;
            } else if (arr[mid] < num) {
                floor = arr[mid];
                start = mid+1;
            } else {
                ceil = floor = arr[mid];
                break;
            }
        }
        System.out.println(ceil);
        System.out.println(floor);
    }
}
```
> `Time Complexity` : **O(log n)**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Ceil and Floor](https://youtu.be/qaQRRWXgFIQ?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>
