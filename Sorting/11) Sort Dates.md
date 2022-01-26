# Sort Dates
Question -> [Sort Dates](https://www.pepcoding.com/resources/online-java-foundation/time-and-space-complexity/sort-dates-official/ojquestion)    

### Implementation
```java
public class Main {
  public static void sortDates(String[] arr) {
    countSort(arr, 1000000, 100, 32); // days
    countSort(arr, 10000, 100, 13); // months
    countSort(arr, 1, 10000, 2501); // years
  }

  public static void countSort(String[] arr,int div, int mod, int range) {
    int[] count = new int[range];
    for(String val: arr) {
        int e = Integer.parseInt(val, 10)/div % mod;
        count[e]++;
    }

    // subtracting 1 in count[0] to make 0 based indexing 
    count[0] = count[0]-1;
    for(int i=1; i<count.length; i++) {
        count[i] += count[i-1];
    }

    String[] output = new String[arr.length];
    for(int i=arr.length-1; i>=0; i--) {
        int e = Integer.parseInt(arr[i], 10)/div % mod;
        output[count[e]] = arr[i];
        count[e]--;
    }
        
    for(int i=0; i<arr.length; i++) {
        arr[i] = output[i];
    }
  }

  public static void print(String[] arr) {
    for (int i = 0; i < arr.length; i++) {
      System.out.println(arr[i]);
    }
  }

  public static void main(String[] args) throws Exception {
    Scanner scn = new Scanner(System.in);
    int n = scn.nextInt();
    String[] arr = new String[n];
    for (int i = 0; i < n; i++) {
      String str = scn.next();
      arr[i] = str;
    }
    sortDates(arr);
    print(arr);
  }
}
```
> `Time Complexity` : **O(n)**, where n = arr.length      
> `Space Complexity` : **O(n)**, where n = arr.length 
---
Video Explanations -> [Sort Dates](https://youtu.be/YdzCuP6LwVg?list=PL-Jc9J83PIiFc7hJ5eeCb579PS8p-en4f)   
<hr>
