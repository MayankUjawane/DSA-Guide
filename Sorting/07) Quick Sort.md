# Partitioning an Array
### Method 1
```java
class QuickSort {
    public static void quickSort(int[] arr, int start, int end) {
        if(start < end) {
            int pivotIndex = partition(arr, start, end);
            quickSort(arr, start, pivotIndex-1);
            quickSort(arr, pivotIndex+1, end);
        }
    }
    
    public static int partition(int[] arr, int start, int end) {
        int pivot = arr[end];
        int i=start;
        int j=start;
        while(i<=end) {
            if(arr[i] > pivot) {
                i++;
            } else {
                // swap arr[i] with arr[j]
                int temp = arr[j];
                arr[j] = arr[i];
                arr[i] = temp;
                i++;
                j++;
            }
        }
        // pivot is at j-1 index
        return j-1;
    }
}
```
### Method 2
```java
class QuickSort {
    public static void quickSort(int[] arr, int start, int end) {
        if(start < end) {
            int pivotIndex = partition(arr, start, end);
            quickSort(arr, start, pivotIndex-1);
            quickSort(arr, pivotIndex+1, end);
        }
    }
    
    public static int partition(int[] arr, int start, int end) {
        int pivot = arr[end];
        int i=start;
        int j=start;
        while(i<=end) {
            if(arr[i] >= pivot) {
                i++;
            } else {
                // swap arr[i] with arr[j]
                int temp = arr[j];
                arr[j] = arr[i];
                arr[i] = temp;
                i++;
                j++;
            }
        }
        //swap arr[end] with arr[j]
        int temp = arr[j];
        arr[j] = arr[end];
        arr[end] = temp;
        // now pivot is at jth index
        return j;
    }
}
```
> `Average Case` : **O(nLogn)**   
> `Worst Case` : **θ(n2)**    
> `Best Case` : **θ(nLogn)**   
> `Auxiliary Space` : **O(n)**     
> `Algorithmic Paradigm` : **Divide and Conquer**     
> `Sorting In Place` : **Yes**         
> As per the broad definition of **in-place algorithm** quick sort qualifies as an **in-place sorting algorithm** as it uses extra space only for storing 
> recursive function calls but not for manipulating the input.            
> `Stable` : **No**        
---  
Video Explanations -> [Quick Sort](https://youtu.be/kdO5Q0nmPjU?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f) 
<hr>
