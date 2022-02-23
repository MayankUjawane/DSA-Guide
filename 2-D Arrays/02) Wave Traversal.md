# Wave Traversal
Question -> [Wave Traversal](https://nados.io/question/the-state-of-wakanda-1?zen=true)    

### Implementation
```java
public class Main{
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int row = sc.nextInt();
        int col = sc.nextInt();
        int[][] arr = new int[row][col];
        for(int i=0; i<row; i++) {
            for(int j=0; j<col; j++) {
                arr[i][j] = sc.nextInt();
            }
        }

        for(int c=0; c<col; c++) {
            if(c%2 == 0) {
                for(int r=0; r<row; r++) {
                    System.out.println(arr[r][c]);
                }
            } else {
                for(int r=row-1; r>=0; r--) {
                    System.out.println(arr[r][c]);
                }
            }
        }
    }
}
```
> `Time Complexity` : **O(Row\*Column)**          
> `Space Complexity` : **O(Row\*Column)**
---
Video Explanations -> [Wave Traversal](https://youtu.be/_olQ9Rrnm_c)   
<hr>
