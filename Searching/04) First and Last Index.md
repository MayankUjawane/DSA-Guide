# First and Last Index
Question -> [First and Last Index](https://www.pepcoding.com/resources/online-java-foundation/function-and-arrays/first-index-last-index-official/ojquestion)    

### Implementation
```java
public class Solution{
    public static void findfirstIndex(int[] arr, int num) {
        int start = 0;
        int end = arr.length-1;
        int firstIndex = -1;
        
        while(start <= end) {
            int mid = (start+end)/2;
            if(arr[mid] > num) {
                end = mid-1;
            } else if (arr[mid] < num) {
                start = mid+1;
            } else {
                firstIndex = mid;
                end = mid-1;
            }
        }
        System.out.println(firstIndex);
    }
    public static void findLastIndex(int[] arr, int num) {
        int start = 0;
        int end = arr.length-1;
        int lastIndex = -1;
        
        while(start <= end) {
            int mid = (start+end)/2;
            if(arr[mid] > num) {
                end = mid-1;
            } else if (arr[mid] < num) {
                start = mid+1;
            } else {
                lastIndex = mid;
                start = mid+1;
            }
        }
        System.out.println(lastIndex);
    }
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for(int i=0; i<n; i++) {
            arr[i] = sc.nextInt();
        }
        int num = sc.nextInt();
        findfirstIndex(arr, num);
        findLastIndex(arr, num);
    }
}
```
> `Time Complexity` : **O((log n) + (log n))**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [First and Last Index](https://youtu.be/9NXZccIWNqU?list=PL-Jc9J83PIiHOV7lm2uSw4ZiVsIRsGS6r)   
<hr>
