# 72.编辑距离
题目链接：[传送门](https://leetcode-cn.com/problems/edit-distance/)

## 题目描述：
给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。
你可以对一个单词进行如下三种操作：
- 插入一个字符
- 删除一个字符
- 替换一个字符

**示例**：

- 输入：`word1 = "horse"`， `word2 = "ros"`
- 输出：`3`
- 解释：

```
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

## 解决方案：
- 时间复杂度：$O(m × n)$
- 空间复杂度：$O(m × n)$
- 思路：记忆化搜索。

## AC代码：
```java
class Solution {
	private int m, n;
	private int[][] dp;
	public int minDistance(String word1, String word2) {
		if (word1 == null || word2 == null)
			return 0;
		m = word1.length();
		n = word2.length();
		dp = new int[m][n];
		return dfs(0, 0, word1, word2);
	}
	private int dfs(int i, int j, String word1, String word2) {
		if (i == m) // i先到达，只能填充word2剩下的字符
			return n - j;
		if (j == n) // j先到达，只能删除word1剩下的字符
			return m - i;
		if (dp[i][j] > 0) // 记忆化
			return dp[i][j];
		int change = 0; // [i:]与[j:]后面编辑的最少次数
		if (word1.charAt(i) == word2.charAt(j))
			change = dfs(i + 1, j + 1, word1, word2);
		else {
			// 插入
			change = dfs(i, j + 1, word1, word2) + 1;
			// 删除
			change = Math.min(change, dfs(i + 1, j, word1, word2) + 1);
			// 替换
			change = Math.min(change, dfs(i + 1, j + 1, word1, word2) + 1);
		}
		// 回溯到这里，再记忆化子问题
		return dp[i][j] = change;
	}
}
```