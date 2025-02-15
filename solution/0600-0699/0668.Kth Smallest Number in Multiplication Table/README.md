# [668. 乘法表中第 k 小的数](https://leetcode.cn/problems/kth-smallest-number-in-multiplication-table)

[English Version](/solution/0600-0699/0668.Kth%20Smallest%20Number%20in%20Multiplication%20Table/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>几乎每一个人都用&nbsp;<a href="https://baike.baidu.com/item/%E4%B9%98%E6%B3%95%E8%A1%A8">乘法表</a>。但是你能在乘法表中快速找到第<code>k</code>小的数字吗？</p>

<p>给定高度<code>m</code>&nbsp;、宽度<code>n</code> 的一张&nbsp;<code>m * n</code>的乘法表，以及正整数<code>k</code>，你需要返回表中第<code>k</code>&nbsp;小的数字。</p>

<p><strong>例&nbsp;1：</strong></p>

<pre>
<strong>输入:</strong> m = 3, n = 3, k = 5
<strong>输出:</strong> 3
<strong>解释:</strong> 
乘法表:
1	2	3
2	4	6
3	6	9

第5小的数字是 3 (1, 2, 2, 3, 3).
</pre>

<p><strong>例 2：</strong></p>

<pre>
<strong>输入:</strong> m = 2, n = 3, k = 6
<strong>输出:</strong> 6
<strong>解释:</strong> 
乘法表:
1	2	3
2	4	6

第6小的数字是 6 (1, 2, 2, 3, 4, 6).
</pre>

<p><strong>注意：</strong></p>

<ol>
	<li><code>m</code> 和&nbsp;<code>n</code>&nbsp;的范围在 [1, 30000] 之间。</li>
	<li><code>k</code> 的范围在 [1, m * n] 之间。</li>
</ol>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：二分查找**

题目可以转换为，求有多少个数不超过 x。对于每一行 i，所有数都是 i 的倍数，不超过 x 的个数有 `x / i` 个。

二分枚举 x，累加每一行不超过 x 的个数，得到 cnt。找到 `cnt >= k` 的最小 x。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def findKthNumber(self, m: int, n: int, k: int) -> int:
        left, right = 1, m * n
        while left < right:
            mid = (left + right) >> 1
            cnt = 0
            for i in range(1, m + 1):
                cnt += min(mid // i, n)
            if cnt >= k:
                right = mid
            else:
                left = mid + 1
        return left
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int left = 1, right = m * n;
        while (left < right) {
            int mid = (left + right) >>> 1;
            int cnt = 0;
            for (int i = 1; i <= m; ++i) {
                cnt += Math.min(mid / i, n);
            }
            if (cnt >= k) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int findKthNumber(int m, int n, int k) {
        int left = 1, right = m * n;
        while (left < right)
        {
            int mid = (left + right) >> 1;
            int cnt = 0;
            for (int i = 1; i <= m; ++i) cnt += min(mid / i, n);
            if (cnt >= k) right = mid;
            else left = mid + 1;
        }
        return left;
    }
};
```

### **Go**

```go
func findKthNumber(m int, n int, k int) int {
	left, right := 1, m*n
	for left < right {
		mid := (left + right) >> 1
		cnt := 0
		for i := 1; i <= m; i++ {
			cnt += min(mid/i, n)
		}
		if cnt >= k {
			right = mid
		} else {
			left = mid + 1
		}
	}
	return left
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```

### **...**

```

```

<!-- tabs:end -->
