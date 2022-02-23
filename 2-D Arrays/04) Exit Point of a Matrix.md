# Exit Point of a Matrix
Question -> [Exit Point of a Matrix](https://nados.io/question/exit-point-of-a-matrix?zen=true)    

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

        int direction = 0;
        int r=0, c=0;

        while (true) {
            direction = (direction + arr[r][c]) % 4;
            //East
            if(direction == 0) {
                c++;
                if(!check(r,c,row,col)) {
                    c--;
                    break;
                }
            }
            //South
            else if(direction == 1) {
                r++;
                if(!check(r,c,row,col)) {
                    r--;
                    break;
                }
            }
            //West
            else if(direction == 2) {
                c--;
                if(!check(r,c,row,col)) {
                    c++;
                    break;
                }    
            }
            //North
            else if(direction == 3) {
                r--;
                if(!check(r,c,row,col)) {
                    r++;
                    break;
                }
            }
        }

        System.out.println(r);
        System.out.println(c);
    }

    public static boolean check(int r, int c, int row, int col) {
        return (r>=0 && c>=0 && r<row && c<col);
    }
}
```
---
Video Explanations -> [Exit Point of a Matrix](https://youtu.be/FUBlb360kqU?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
