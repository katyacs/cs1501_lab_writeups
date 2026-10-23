# Lab 6
## Code

```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
     //check if starting pixel's color is color, then return
     if(image[sr][sc] == color)
        return image;
     int startColor = image[sr][sc];
     //get size of matrix
     int rows = image.length;
     int cols = image[0].length;

     image[sr][sc] = color;

     image = floodFill(image, sr+1, sc, startColor,color,rows,cols);
     image = floodFill(image, sr-1, sc, startColor,color,rows,cols);
     image = floodFill(image, sr, sc+1, startColor,color,rows,cols);
     image = floodFill(image, sr, sc-1, startColor,color,rows,cols);

     return image;
    }

    private int[][] floodFill(int[][] image, int sr, int sc, int startColor, int color, int rows, int cols)
    {
        //check if sr and sc are in bounds
        if(sr > rows-1 || sr < 0 || sc > cols-1 || sc < 0)
            return image;
        //check if new pixel is equal to start color, if not return
        if(image[sr][sc] != startColor)
            return image;

        image[sr][sc] = color;

        image = floodFill(image, sr+1, sc, startColor,color,rows,cols);
        image = floodFill(image, sr-1, sc, startColor,color,rows,cols);
        image = floodFill(image, sr, sc+1, startColor,color,rows,cols);
        image = floodFill(image, sr, sc-1, startColor,color,rows,cols);

        return image;
    }
}
```

## Description:
For this problem, we got a matrix containing color values of image pixels. We had to change the color of the starting pixel and the pixels surrounding it that are also the same starting color, essentially filling in a section of color with the provided color. To do this, I used a recursive helper function. Initially
## Runtime Analysis: 

## Space Complexity:
