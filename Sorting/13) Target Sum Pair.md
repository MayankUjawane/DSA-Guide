# Target Sum Pair
Question -> [Target Sum Pair](https://www.pepcoding.com/resources/online-java-foundation/time-and-space-complexity/target-sum-pair-1-official/ojquestion)    

### Implementation
```java
public class Solution {
    public static void targetSumPair(int[] arr, int target) {
        Arrays.sort(arr);
        int low = 0;
        int high = arr.length-1;
        while(low < high) {
            int sum = arr[low] + arr[high];
            if(sum == target) {
                System.out.println(arr[low] + ", " + arr[high]);
                low++;
                high--;
            } else if (sum > target) {
                high--;
            } else {
                low++;
            }
        }
    }
}
```
> `Time Complexity` : **O(NlogN)**     
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Target Sum Pair](https://youtu.be/4t9jv9AkVdE?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f)   
<hr>
