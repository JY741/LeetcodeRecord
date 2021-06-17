# 面试题 01.07.旋转矩阵
题目链接：[传送门](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

## 题目描述：
给定一幅由N × N矩阵表示的图像，其中每个像素的大小为4字节，编写一种方法，将图像旋转90度。
不占用额外内存空间能否做到？

## 解决方案：
- 时间复杂度：$O(m × n)$
- 空间复杂度：$O(1)$
- 思路：先沿着正对角线翻折交换，再对着正中线翻折交换即可！

## AC代码：
```java
class Solution {
	public void rotate(int[][] matrix) {
		int m, n;
		if (matrix == null || (m = matrix.length) == 0 || (n = matrix[0].length) == 0)
			return;
		for (int i = 1; i < m; i++)
			for (int j = 0; j <= i; j++)
				swap(matrix, i, j, j, i);
		for (int i = 0, colL = n / 2; i < m; i++)
			for (int j = 0; j < colL; j++)
				swap(matrix, i, j, i, n - 1 - j);
	}
	private void swap(int[][] matrix, int i, int j, int a, int b) {
		if (matrix[i][j] == matrix[a][b])
			return;
		matrix[i][j] ^= matrix[a][b];
		matrix[a][b] ^= matrix[i][j];
		matrix[i][j] ^= matrix[a][b];
	}
}
```