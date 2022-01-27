# Bar Chart
Question -> [Bar Chart](https://www.pepcoding.com/resources/online-java-foundation/function-and-arrays/bar-chart-official/ojquestion)    

### Implementation
```java
public class Solution{
    public void barChart(int[] arr, int n) {
        int max = arr[0];
        for(int i=1; i<n; i++) {
            if(arr[i] > max) {
                max = arr[i];
            }
        }
        for(int i=max; i>0; i--) {
            for(int j=0; j<n; j++) {
                if(arr[j] >= i) {
                    System.out.print("*\t");
                } else {
                    System.out.print("\t");
                }
            }
            System.out.println();
        }
    }  
}
```
> `Time Complexity` : **O(m*n)**, where m = max element in array and n = number of elements in array       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Bar Chart](https://youtu.be/L-0IxqvYQKs?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>
