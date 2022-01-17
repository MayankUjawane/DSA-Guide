# Bubble Sort

```java
void bubbleSort(int arr[]) {
    int n = arr.length;
    for (int i = 0; i < n-1; i++) {
        boolean swap = false;
        //for every ith iteration, end ith elements will get sorted for sure that's why we are running inner loop for 'n-i-1' times.
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                // swap arr[j+1] and arr[j]
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                swap = true;
            }
        }
        // If no two elements were swapped by inner loop, then break.
        if(swap == false) {
            break;
        }
    }
}
```
> `Worst and Average Case Time Complexity` : **O(n*n)**, Worst case occurs when array is reverse sorted.         
> `Best Case Time Complexity` : **O(n)**, Best case occurs when array is already sorted.                   
> `Auxiliary Space` : **O(1)**            
> `Sorting In Place` : **Yes**           
> `Stable` : **Yes**   
---
Video Explanations -> Bubble Sort - [Pepcoding](https://youtu.be/Jv-eGC2xmtU?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f), [GFG](https://youtu.be/nmhjrI-aW5o) 
<hr>
