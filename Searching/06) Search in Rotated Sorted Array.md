# Search in Rotated Sorted Array
Question -> [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)    

### O(2(log n)) Approach
```java
public class Solution{
    public int search(int[] arr, int target) {
        int pivotIndex = findPivot(arr);
        if(target == arr[pivotIndex]) return pivotIndex;
        
        int end = arr.length-1;
        if(target > arr[pivotIndex] && target <= arr[end]) {
            return binarySearch(arr, pivotIndex+1, end, target);
        } else {
            return binarySearch(arr, 0, pivotIndex-1, target);
        }
    }
    public int findPivot(int[] arr) {
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
        return start;
    }
    public int binarySearch(int[] arr, int start, int end, int target) {
        while(start <= end) {
            int mid = (start+end)/2;
            
            if(arr[mid] == target) {
                return mid;
            } else if(arr[mid] > target) {
                end = mid-1;
            } else {
                start = mid+1;
            }
        }
        return -1;
    }
}
```
> `Time Complexity` : **O((log n) + (log n))**       
> `Space Complexity` : **O(1)**
---
### O(log n) Approach
```java
public class Solution{
    public int search(int[] arr, int target) {
        int start = 0;
        int end = arr.length-1;
        while(start <= end) {
            int mid = (start+end)/2;
            
            if(arr[mid] == target) {
                return mid;
            }
            // we are checking arr[mid] >= arr[start] for edge case when mid == start
            else if(arr[mid] >= arr[start]) {
                if(target >= arr[start] && target < arr[mid]) {
                    end = mid-1;
                } else {
                    start = mid+1;
                }
            } else {
                if(target > arr[mid] && target <= arr[end]) {
                    start = mid+1;
                } else {
                    end = mid-1;
                }
            }
        }
        return -1;
    }
}
```
> `Time Complexity` : **O(log n)**       
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Search in Rotated Sorted Array](https://youtu.be/oTfPJKGEHcc)   
<hr>
