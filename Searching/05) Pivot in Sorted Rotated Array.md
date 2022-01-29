# Pivot in Sorted Rotated Array
Question -> [Pivot in Sorted Rotated Array](https://www.pepcoding.com/resources/online-java-foundation/time-and-space-complexity/pivot-sorted-rotated-array-official/ojquestion)    

### Implementation
```java
public class Solution{
    public static int findPivot(int[] arr) {
        int start = 0;
        int end = arr.length-1; 
        while(start < end) {
            int mid = (start+end)/2;
            if(arr[mid] > arr[end]) {
                start = mid+1;
            } else {
                end = mid;
            }
        }
        return arr[start];
    }

    public static void main(String[] args) throws Exception {
        Scanner scn = new Scanner(System.in);
        int n = scn.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
          arr[i] = scn.nextInt();
        }
        int pivot = findPivot(arr);
        System.out.println(pivot);
    }
}
```
> `Time Complexity` : **O(log n)**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Pivot in Sorted Rotated Array](https://youtu.be/vF7gk4iaklA?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f)   
<hr>
