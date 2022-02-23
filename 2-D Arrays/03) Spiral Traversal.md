# Spiral Traversal
Question -> [Spiral Traversal](https://nados.io/question/spiral-display?zen=true)    

### Implementation
```java
public class Main {
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

        int minr=0, minc=0, maxr=arr.length-1, maxc = arr[0].length-1;
        int totalElements = row*col, count=0;

        while(count < totalElements) {
            //left wall
            for(int r=minr; r<=maxr && count<totalElements; r++) {
                System.out.println(arr[r][minc]);
                count++;
            }
            minc++;

            //bottom wall
            for(int c=minc; c<=maxc && count<totalElements; c++) {
                System.out.println(arr[maxr][c]);
                count++;
            }
            maxr--;

            //right wall
            for(int r=maxr; r>=minr && count<totalElements; r--) {
                System.out.println(arr[r][maxc]);
                count++;
            }
            maxc--;

            //top wall
            for(int c=maxc; c>=minc && count<totalElements; c--) {
                System.out.println(arr[minr][c]);
                count++;
            }
            minr++;
        }
    }
}
```
> `Time Complexity` : **O(Row\*Column)**         
> `Space Complexity` : **O(Row\*Column)**
---
Video Explanations -> [Spiral Traversal](https://youtu.be/SVFXEqn3Ceo?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
