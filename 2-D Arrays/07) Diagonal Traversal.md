# Diagonal Traversal
Question -> [Diagonal Traversal](https://nados.io/question/the-state-of-wakanda-2?zen=true)    

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

        for(int gap=0; gap<n; gap++) {
            int c=gap;
            for(int r=0; r<n-gap; r++) {
                System.out.println(arr[r][c]);
                c++;
            }
        }
    }
}
```
---
Video Explanations -> [Diagonal Traversal](https://youtu.be/lvRdFCMD_Ew?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
