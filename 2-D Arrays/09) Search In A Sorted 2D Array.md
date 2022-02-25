# Search In A Sorted 2D Array
Question -> [Search In A Sorted 2D Array](https://nados.io/question/search-in-a-sorted-2d-array?zen=true)    

### Implementation
```java
public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] arr = new int[n][n];
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                arr[i][j] = sc.nextInt();
            }
        }
        int number = sc.nextInt();

        int maxc = n-1;
        for(int r=0; r<n; r++) {
            if(number > arr[r][maxc]) continue;
            for(int c=0; c<n; c++) {
                if(number == arr[r][c]) {
                    System.out.println(r);
                    System.out.println(c);
                    return;
                }
            }
            break;
        }
        System.out.println("Not Found");
    }
}
```
---
Video Explanations -> [Search In A Sorted 2D Array](https://youtu.be/5vP0-g94xEA?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
