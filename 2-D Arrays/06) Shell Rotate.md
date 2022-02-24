# Shell Rotate
Question -> [Shell Rotate](https://nados.io/question/ring-rotate?zen=true)    

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
        int s = sc.nextInt();
        int r = sc.nextInt();
        rotateShell(arr, s, r);
        display(arr);
    }
    
    public static void rotateShell(int[][] arr, int s, int r) {
        int[] onedArray = fillOnedArrayFromShell(arr, s);
        rotateOnedArray(onedArray, r);
        fillShellFromOned(onedArray, arr, s);
    }
    
    public static int[] fillOnedArrayFromShell(int[][] arr, int s) {
        int minr = s-1, maxr = arr.length-s;
        int minc = s-1, maxc = arr[0].length-s;

        int size = 2*(maxr-minr+1) + 2*(maxc-minc+1) - 4;
        int[] oned = new int[size];
        int ind = 0;

        //left wall
        for(int r=minr; r<=maxr; r++) {
            oned[ind++] = arr[r][minc];
        }
        //bottom wall
        for(int c=minc+1; c<=maxc; c++) {
            oned[ind++] = arr[maxr][c];
        }
        //right wall
        for(int r=maxr-1; r>=minr; r--) {
            oned[ind++] = arr[r][maxc];
        }
        //top wall
        for(int c=maxc-1; c>=minc+1; c--) {
            oned[ind++] = arr[minr][c];
        }

        return oned;
    }
    
    public static void rotateOnedArray(int[] oned, int r) {
        r = r % oned.length;
        if(r < 0) {
            r = oned.length + r;
        }

        reverse(oned, 0, oned.length-r-1);
        reverse(oned, oned.length-r, oned.length-1);
        reverse(oned, 0, oned.length-1);
    }

    public static void reverse(int[] oned, int li, int ri) {
        while(li < ri) {
            int temp = oned[ri];
            oned[ri] = oned[li];
            oned[li] = temp;
            li++;
            ri--;
        }
    }

    public static void fillShellFromOned(int[] oned, int[][] arr, int s) {
        int minr = s-1, maxr = arr.length-s;
        int minc = s-1, maxc = arr[0].length-s;
        int ind = 0;

        //left wall
        for(int r=minr; r<=maxr; r++) {
            arr[r][minc] = oned[ind++];
        }
        //bottom wall
        for(int c=minc+1; c<=maxc; c++) {
            arr[maxr][c] = oned[ind++];
        }
        //right wall
        for(int r=maxr-1; r>=minr; r--) {
            arr[r][maxc] = oned[ind++];
        }
        //top wall
        for(int c=maxc-1; c>=minc+1; c--) {
            arr[minr][c] = oned[ind++];
        }
    }

    public static void display(int[][] arr) {
        for(int i = 0; i < arr.length; i++){
            for(int j = 0; j < arr[0].length; j++){
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```
---
Video Explanations -> [Shell Rotate](https://youtu.be/atMK9aA-s7Y?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
