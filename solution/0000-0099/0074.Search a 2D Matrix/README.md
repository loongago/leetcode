# [74. 搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix)

[English Version](/solution/0000-0099/0074.Search%20a%202D%20Matrix/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->
<p>编写一个高效的算法来判断&nbsp;<em>m</em> x <em>n</em>&nbsp;矩阵中，是否存在一个目标值。该矩阵具有如下特性：</p>

<ul>
	<li>每行中的整数从左到右按升序排列。</li>
	<li>每行的第一个整数大于前一行的最后一个整数。</li>
</ul>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入:</strong>
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
<strong>输出:</strong> true
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre><strong>输入:</strong>
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
<strong>输出:</strong> false</pre>

## 解法

<!-- 这里可写通用的实现逻辑 -->

将二维矩阵逻辑展开，然后二分查找即可。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        l, h = 0, m * n - 1
        while l <= h:
            mid = (l + h) >> 1
            x, y = divmod(mid, n)
            if matrix[x][y] == target:
                return True
            if matrix[x][y] < target:
                l = mid + 1
            else:
                h = mid - 1
        return False
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int l = 0, h = m * n - 1;
        while (l <= h) {
            int mid = (l + h) >>> 1;
            int x = mid / n, y = mid % n;
            if (matrix[x][y] == target) return true;
            if (matrix[x][y] < target) l = mid + 1;
            else h = mid - 1;
        }
        return false;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int l = 0, h = m * n - 1;
        while (l <= h) {
            int mid = l + ((h - l) >> 1);
            int x = mid / n, y = mid % n;
            if (matrix[x][y] == target) return true;
            if (matrix[x][y] < target) l = mid + 1;
            else h = mid - 1;
        }
        return false;
    }
};
```

### **...**

```

```

<!-- tabs:end -->
