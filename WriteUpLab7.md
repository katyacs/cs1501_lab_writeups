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
For this problem, we got a matrix containing color values of image pixels. We had to change the color of the starting pixel and the pixels surrounding it that are also the same starting color, essentially filling in a section of color with the provided color. To do this, I used a recursive helper function. Initially, the main method checks whether the starting pixel already has the target color and returns the image unchanged.Otherwise, it saves the starting color, recolors the starting pixel, and calls the helper on its four neighbors. The helper first checks that the pixel is in bounds and that it still matches the starting color. If either check fails, it returns. If they pass, it recolors the pixel and recursively calls itself on the four neighbors.

## Runtime Analysis: 
My program has a runtime of O(n) where n is the number of pixels visited. There is a constant amount of work done on each pixel, so runtime only depends on how many pixels are visited. This could range from one pixel in the best case and every pixel (the entire matrix) in the worst case.

## Space Complexity:
I don't create a new matrix, but my helper method calls take up space. This is also linear O(n) where n is the number of pixels visited by the helper method.
