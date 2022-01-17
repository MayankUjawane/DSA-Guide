# Merge Two Sorted Arrays

```java
public void merge(int[] a, int[] b) {
    int[] res = new int[a.length + b.length];
    int i=0, j=0, k=0;

    while(i<a.length && j<b.length) {
        if(a[i] < b[j]) {
            res[k] = a[i];
            i++;
            k++;
        } else {
            res[k] = b[j];
            j++;
            k++;
        }
    }

    while(i<a.length) {
        res[k] = a[i];
        k++;
        i++;
    }

    while(j<b.length) {
        res[k] = b[j];
        k++;
        j++;
    }
}
```
> `Time Complexity` : **O(n)**   
> `Auxiliary Space` : **O(n)**     
---
Video Explanations -> [Merge Two Sorted Arrays](https://youtu.be/WMxNhIBA92I?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f) 
<hr>
