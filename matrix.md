# Matrix

### Search a 2D Matrix

```
Write an efficient algorithm that searches for a value in an m x n matrix. 
This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer 
of the previous row

Input: 
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

Output: true
```

```java
class Solution {
	public boolean searchMatrix(int[][] matrix, int target) {
		int start = 0;
		int last = matrix[0].length - 1;

		while (last >= 0 && start < matrix.length) {
			if (matrix[start][last] < target)
				start++;
			else if (matrix[start][last] > target)
				last--;
			else
				return true;
		}

		return false;
	}
}
```

### Flood Fill

```
An image is represented by an m x n integer grid image 
where image[i][j] represents the pixel value of the image.

You are also given three integers sr, sc, and newColor. 
You should perform a flood fill on the image starting 
from the pixel image[sr][sc].

To perform a flood fill, consider the starting pixel, 
plus any pixels connected 4-directionally to the starting pixel 
of the same color as the starting pixel, 
plus any pixels connected 4-directionally to those pixels 
(also with the same color), and so on. 

Replace the color of all of the aforementioned pixels with newColor.

Return the modified image after performing the flood fill.
```

```java
class Solution {
	public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
		int color = image[sr][sc];
		if (color != newColor)
			dfs(image, sr, sc, color, newColor);
		return image;
	}

	public void dfs(int[][] image, int r, int c, int color, int newColor) {
		if (image[r][c] == color) {
			image[r][c] = newColor;
			if (r >= 1)
				dfs(image, r - 1, c, color, newColor);
			if (c >= 1)
				dfs(image, r, c - 1, color, newColor);
			if (r + 1 < image.length)
				dfs(image, r + 1, c, color, newColor);
			if (c + 1 < image[0].length)
				dfs(image, r, c + 1, color, newColor);
		}
	}
}
```

### Max Area of Island

```
You are given an m x n binary matrix grid. 
An island is a group of 1's (representing land) connected 4-directionally 
(horizontal or vertical.) You may assume all four edges of the 
grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.
```

```java
class Solution {
	int[][] grid;
	boolean[][] seen;

	public int area(int r, int c) {
		if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length ||
				seen[r][c] || grid[r][c] == 0)
			return 0;
		seen[r][c] = true;
		return (1 + area(r + 1, c) + area(r - 1, c)
				+ area(r, c - 1) + area(r, c + 1));
	}

	public int maxAreaOfIsland(int[][] grid) {
		this.grid = grid;
		seen = new boolean[grid.length][grid[0].length];
		int ans = 0;
		for (int r = 0; r < grid.length; r++) {
			for (int c = 0; c < grid[0].length; c++) {
				ans = Math.max(ans, area(r, c));
			}
		}
		return ans;
	}
}
```

### Reshape the Matrix

```java
In MATLAB, there is a handy function called reshape which 
    can reshape an m x n matrix into a new one with a 
    different size r x c keeping its original data.

You are given an m x n matrix mat and two integers r and c 
    representing the number of rows and the 
    number of columns of the wanted reshaped matrix.
    
Input: mat = [[1,2],[3,4]], r = 1, c = 4
Output: [[1,2,3,4]
```

```java
class Solution {
	public int[][] matrixReshape(int[][] mat, int r, int c) {
		int n = mat.length;
		int m = mat[0].length;

		if ((n * m) != (r * c))
			return mat;

		int[][] ans = new int[r][c];
		int k = 0, l = 0;

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < m; j++) {
				if (l >= c) {
					l = 0;
					k++;
				}
				ans[k][l++] = mat[i][j];
			}
		}
		return ans;
	}
}
```

### Pascal's Triangle

```java
Example 1:

Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
	public List<List<Integer>> generate(int numRows) {
		List<List<Integer>> triangle = new ArrayList<>();

		if (numRows == 0)
			return triangle;
		List<Integer> firstRow = new ArrayList<>();
		firstRow.add(1);
		triangle.add(firstRow);

		for (int i = 1; i < numRows; i++) {
			List<Integer> prevRow = triangle.get(i - 1);
			List<Integer> row = new ArrayList<>();

			row.add(1);
			for (int j = 1; j < i; j++) {
				row.add(prevRow.get(j - 1) + prevRow.get(j));
			}
			row.add(1);
			triangle.add(row);
		}
		return triangle;
	}
}
```



### Boundary traversal of matrix

```java

class Solution {
	public static void printBoundary(int a[][], int m, int n) {
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < n; j++) {
			if (i == 0)
				System.out.print(a[i][j] + " ");
			else if (i == m - 1)
				System.out.print(a[i][j] + " ");
			else if (j == 0)
				System.out.print(a[i][j] + " ");
			else if (j == n - 1)
				System.out.print(a[i][j] + " ");
			else
				System.out.print("  ");
		}
		System.out.println("");
	}
	}

	public static void main(String[] args) {
		int a[][] = {
				{ 1, 2, 3, 4 },
				{ 5, 6, 7, 8 },
				{ 1, 2, 3, 4 },
				{ 5, 6, 7, 8 }
		};
		printBoundary(a, 4, 4);
	}
}
```

### Spirally traversing of matrix

```java

class Solution {
	// Function print matrix in spiral form
	static void spiralPrint(int m, int n, int a[][]) {
	int i, k = 0, l = 0;

	// k - starting row index
	// m - ending row index
	// l - starting column index
	// n - ending column index
	// i - iterator

	while (k < m && l < n) {
		// Print the first row from the
		// remaining rows
		for (i = l; i < n; ++i) {
			System.out.print(a[k][i] + " ");
		}
		k++;
		// Print the last column from the
		// remaining columns
		for (i = k; i < m; ++i) {
			System.out.print(a[i][n - 1] + " ");
		}
		n--;
		// Print the last row from the
		// remaining rows
		if (k < m) {
			for (i = n - 1; i >= l; --i) {
				System.out.print(a[m - 1][i] + " ");
			}
			m--;
		}
		// Print the first column from the
		// remaining columns
		if (l < n) {
			for (i = m - 1; i >= k; --i) {
				System.out.print(a[i][l] + " ");
			}
			l++;
		}
	}
	}

	// driver program
	public static void main(String[] args) {
	int R = 3;
	int C = 6;
	int a[][] = {
			{ 1, 2, 3, 4, 5, 6 },
			{ 7, 8, 9, 10, 11, 12 },
			{ 13, 14, 15, 16, 17, 18 }
	};
	spiralPrint(R, C, a);
	}
}
```



### Adding two matrices

```java
public class Solution {

static int[][] sumMatrix(int a[][], int b[][]) {
	int n1 = a.length, n2 = b.length;
	int m1 = a[0].length, m2 = b[0].length;
	int arr[][] = new int[n1][m1];

	if (n1 == n2 && m1 == m2) {
		for (int i = 0; i < a.length; i++) {
			for (int j = 0; j < a[i].length; j++) {
				arr[i][j] = a[i][j] + b[i][j];
			}
		}
	} else {
		return new int[][] {};
	}

	return arr;
}
}
```

### Sum of upper and lower triangles

```java
import java.util.ArrayList;

/**
 * Solution
 */
public class Solution {

static ArrayList<Integer> sumTriangles(int matrix[][], int n) {
	ArrayList<Integer> arrlst = new ArrayList<>();
	int uppertrig = 0;
	int lowertrig = 0;
	for (int i = 0; i < matrix.length; i++) {
		for (int j = 0; j < matrix.length; j++) {
			if (j >= i) {
				uppertrig += matrix[i][j];
			}
			if (j <= i) {
				lowertrig += matrix[i][j];
			}
		}
	}

	arrlst.add(uppertrig);
	arrlst.add(lowertrig);

	return arrlst;
}
}
```

### Matrix Multiplication

```java
public class Solution {
	public static void main(String args[]) {
		
	int a[][] = { { 1, 1, 1 }, { 2, 2, 2 }, { 3, 3, 3 } };
	int b[][] = { { 1, 1, 1 }, { 2, 2, 2 }, { 3, 3, 3 } };
	
	int c[][] = new int[3][3]; 
	
	for (int i = 0; i < 3; i++) {
		for (int j = 0; j < 3; j++) {
			c[i][j] = 0;
			for (int k = 0; k < 3; k++) {
				c[i][j] += a[i][k] * b[k][j];
			} 
			System.out.print(c[i][j] + " "); 
		} 
		System.out.println();
	}
	}
}
```

### Print matrix in snake pattern

```java
public class Solution {
	static void print(int[][] mat) {
	// Traverse through all rows
	for (int i = 0; i < mat.length; i++) {

		// If current row is even, print from
		// left to right
		if (i % 2 == 0) {
			for (int j = 0; j < mat[0].length; j++)
				System.out.print(mat[i][j] + " ");
			System.out.println();
			// If current row is odd, print from
			// right to left
		} else {
			for (int j = mat[0].length - 1; j >= 0; j--)
				System.out.print(mat[i][j] + " ");
			System.out.println();
		}
	}
	}

	public static void main(String[] args) {
		int[][] mat = {
				{ 10, 20, 30, 40 },
				{ 15, 25, 35, 45 },
				{ 27, 29, 37, 48 },
				{ 32, 33, 39, 50 }
		};
		print(mat);
	}
}
```

### Transpose without extra space

```java
// Function to find transpose of a matrix.
static void swap(int mat[][], int i, int j) {
	int temp = mat[i][j];
	mat[i][j] = mat[j][i];
	mat[j][i] = temp;
}

static void transpose(int matrix[][], int n) {
	// code here
	for (int i = 0; i < n; i++) {
		for (int j = i; j < n; j++) {
			swap(matrix, i, j);
		}
	}
}
```

### Rotate by 90 degree

```cpp
void rotateby90(vector<vector<int> >& matrix, int n) 
{ 
   // code here 
   for(int i=0;i<n;i++){
       for(int j=0;j<i;j++){
           swap(matrix[i][j],matrix[j][i]);
       }
   }
   for(int i=0;i<n/2;i++){
       for(int j=0;j<n;j++){
           swap(matrix[i][j],matrix[n-1-i][j]);
       }
   }
} 
```

### Reversing the columns of a Matrix

```
Input:

R = 4, C = 3
matrix[][] = {
	{ 1, 0, 0},
    { 1, 0, 0},
	{ 1, 0, 0},
	{ 0, 0, 0}
}

Output: 
1 1 1
1 1 1
1 1 1
1 0 0 

Explanation:

The position of cells that have 1 in
the original matrix are (0,0), (1,0)
and (2,0). Therefore, all cells in row
0,1,2 are and column 0 are modified to 1. 
```

```java
static void reverseCol(int matrix[][])
{
   // code here 
   for(int i=0;i<matrix.length;i++){
       for(int j=0;j<matrix[i].length/2;j++){
           int temp=matrix[i][j];
           matrix[i][j]=matrix[i][matrix[i].length-j-1];
           matrix[i][matrix[i].length-j-1]=temp;
       }
   }
}
```

### Boolean Matrix

```java
class Solution {
	public static void modifyMatrix(int mat[][]) {

		// variables to check if there are any 1
		// in first row and column
		boolean row_flag = false;
		boolean col_flag = false;

		// updating the first row and col if 1
		// is encountered
		for (int i = 0; i < mat.length; i++) {
			for (int j = 0; j < mat[0].length; j++) {
				if (i == 0 && mat[i][j] == 1)
					row_flag = true;

				if (j == 0 && mat[i][j] == 1)
					col_flag = true;

				if (mat[i][j] == 1) {

					mat[0][j] = 1;
					mat[i][0] = 1;
				}
			}
		}

		// Modify the input matrix mat[] using the
		// first row and first column of Matrix mat
		for (int i = 1; i < mat.length; i++) {
			for (int j = 1; j < mat[0].length; j++) {
				if (mat[0][j] == 1 || mat[i][0] == 1) {
					mat[i][j] = 1;
				}
			}
		}

		// modify first row if there was any 1
		if (row_flag == true) {
			for (int i = 0; i < mat[0].length; i++) {
				mat[0][i] = 1;
			}
		}

		// modify first col if there was any 1
		if (col_flag == true) {
			for (int i = 0; i < mat.length; i++) {
				mat[i][0] = 1;
			}
		}
	}

	/* A utility function to print a 2D matrix */
	public static void printMatrix(int mat[][]) {
		for (int i = 0; i < mat.length; i++) {
			for (int j = 0; j < mat[0].length; j++) {
				System.out.print(mat[i][j]);
			}
			System.out.println("");
		}
	}

	// Driver function to test the above function
	public static void main(String args[]) {

		int mat[][] = {
				{ 1, 0, 0, 1 },
				{ 0, 0, 1, 0 },
				{ 0, 0, 0, 0 }
		};

		System.out.println("Input Matrix :");
		printMatrix(mat);

		modifyMatrix(mat);

		System.out.println("Matrix After Modification :");
		printMatrix(mat);

	}
}
```

### Make matrix beautiful

```
Input:

N = 3
matrix[][] = {
	{1, 2, 3},
    {4, 2, 3},
    {3, 2, 1}
}

Output: 6

Explanation:

Original matrix is as follows:
1 2 3
4 2 3
3 2 1

We need to make increment in such a way 
that each row and column has one time 2, 
one time 3 , one time 4. For that we 
need 6 operations
```

```java
import java.util.Arrays;

class Solution {
	// Function to find minimum number of operations that are required
	// to make the matrix beautiful.
static int findMinOperation(int matrix[][], int n)
{
    int sumRow[] = new int[n];
    int sumCol[] = new int[n];
    Arrays.fill(sumRow, 0);
    Arrays.fill(sumCol, 0);
    
    //calculating sumRow[] and sumCol[] array.
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            sumRow[i] += matrix[i][j];
            sumCol[j] += matrix[i][j];
              
        }
    }
    
    //finding maximum sum value in either row or in column.
    int maxSum = 0;
    for (int i = 0; i < n; ++i)
    {
        maxSum = Math.max(maxSum, sumRow[i]);
        maxSum = Math.max(maxSum, sumCol[i]);
    } 
    
    int count = 0;
    for (int i = 0, j = 0; i < n && j < n;) 
    {
        //finding minimum increment required in either row or column.
        int diff = Math.min(maxSum - sumRow[i], maxSum - sumCol[j]);
        
        //adding difference in corresponding cell, 
        //sumRow[] and sumCol[] array.
        matrix[i][j] += diff;
        sumRow[i] += diff;
        sumCol[j] += diff;
        
        //updating the result.
        count += diff;
        
        //if ith row is satisfied, incrementing i for next iteration.
        if (sumRow[i] == maxSum)
            ++i;
        
        //if jth column is satisfied, incrementing j for next iteration.
        if (sumCol[j] == maxSum)
            ++j;
    }
    //returning the result.
    return count;
}
```

### Unique rows in boolean matrix

```markdown
Input:

row = 3, col = 4 
M[][] = {
	{1 1 0 1},
	{1 0 0 1},
	{1 1 0 1}
}

Output: '1 1 0 1' & '1 0 0 1'

Explanation: 
Above the matrix of size 3x4 looks like
1 1 0 1
1 0 0 1
1 1 0 1

The two unique rows are 1 1 0 1 and 1 0 0 1.
```

```java
import java.util.HashSet;

public class Solution {

	public static void printArray(int arr[][], int row, int col) {

		HashSet<String> set = new HashSet<String>();

		for (int i = 0; i < row; i++) {
			String s = "";

			for (int j = 0; j < col; j++)
				s += String.valueOf(arr[i][j]);

			if (!set.contains(s)) {
				set.add(s);
				System.out.println(s);
			}
		}
	}

	// Driver code
	public static void main(String[] args) {

		int arr[][] = {
				{ 0, 1, 0, 0, 1 },
				{ 1, 0, 1, 1, 0 },
				{ 0, 1, 0, 0, 1 },
				{ 1, 1, 1, 0, 0 }
		};

		printArray(arr, 4, 5);
	}
}
```
