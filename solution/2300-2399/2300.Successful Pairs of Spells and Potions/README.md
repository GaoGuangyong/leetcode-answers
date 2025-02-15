# [2300. 咒语和药水的成功对数](https://leetcode.cn/problems/successful-pairs-of-spells-and-potions)

[English Version](/solution/2300-2399/2300.Successful%20Pairs%20of%20Spells%20and%20Potions/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你两个正整数数组&nbsp;<code>spells</code> 和&nbsp;<code>potions</code>&nbsp;，长度分别为&nbsp;<code>n</code> 和&nbsp;<code>m</code>&nbsp;，其中&nbsp;<code>spells[i]</code>&nbsp;表示第&nbsp;<code>i</code>&nbsp;个咒语的能量强度，<code>potions[j]</code>&nbsp;表示第&nbsp;<code>j</code>&nbsp;瓶药水的能量强度。</p>

<p>同时给你一个整数&nbsp;<code>success</code>&nbsp;。一个咒语和药水的能量强度 <strong>相乘</strong> 如果&nbsp;<strong>大于等于</strong>&nbsp;<code>success</code>&nbsp;，那么它们视为一对&nbsp;<strong>成功</strong>&nbsp;的组合。</p>

<p>请你返回一个长度为 <code>n</code>&nbsp;的整数数组<em>&nbsp;</em><code>pairs</code>，其中<em>&nbsp;</em><code>pairs[i]</code>&nbsp;是能跟第 <code>i</code>&nbsp;个咒语成功组合的 <b>药水</b>&nbsp;数目。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><b>输入：</b>spells = [5,1,3], potions = [1,2,3,4,5], success = 7
<b>输出：</b>[4,0,3]
<strong>解释：</strong>
- 第 0 个咒语：5 * [1,2,3,4,5] = [5,<em><strong>10</strong></em>,<em><strong>15</strong></em>,<em><strong>20</strong></em>,<em><strong>25</strong></em>] 。总共 4 个成功组合。
- 第 1 个咒语：1 * [1,2,3,4,5] = [1,2,3,4,5] 。总共 0 个成功组合。
- 第 2 个咒语：3 * [1,2,3,4,5] = [3,6,<em><strong>9</strong></em>,<em><strong>12</strong></em>,<em><strong>15</strong></em>] 。总共 3 个成功组合。
所以返回 [4,0,3] 。
</pre>

<p><strong>示例 2：</strong></p>

<pre><b>输入：</b>spells = [3,1,2], potions = [8,5,8], success = 16
<b>输出：</b>[2,0,2]
<strong>解释：</strong>
- 第 0 个咒语：3 * [8,5,8] = [<em><strong>24</strong></em>,15,<em><strong>24</strong></em>] 。总共 2 个成功组合。
- 第 1 个咒语：1 * [8,5,8] = [8,5,8] 。总共 0 个成功组合。
- 第 2 个咒语：2 * [8,5,8] = [<em><strong>16</strong></em>,10,<em><strong>16</strong></em>] 。总共 2 个成功组合。
所以返回 [2,0,2] 。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>n == spells.length</code></li>
	<li><code>m == potions.length</code></li>
	<li><code>1 &lt;= n, m &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= spells[i], potions[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= success &lt;= 10<sup>10</sup></code></li>
</ul>


## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：二分查找**

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def successfulPairs(self, spells: List[int], potions: List[int], success: int) -> List[int]:
        potions.sort()
        m = len(potions)
        ans = []
        for s in spells:
            left, right = 0, m
            while left < right:
                mid = (left + right) >> 1
                if s * potions[mid] >= success:
                    right = mid
                else:
                    left = mid + 1
            ans.append(m - left)
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int[] successfulPairs(int[] spells, int[] potions, long success) {
        Arrays.sort(potions);
        int m = potions.length, n = spells.length;
        int[] ans = new int[n];
        for (int i = 0; i < n; ++i) {
            int left = 0, right = m;
            while (left < right) {
                int mid = (left + right) >> 1;
                if ((long) spells[i] * potions[mid] >= success) {
                    right = mid;
                } else {
                    left = mid + 1;
                }
            }
            ans[i] = m - left;
        }
        return ans;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<int> successfulPairs(vector<int>& spells, vector<int>& potions, long long success) {
        sort(potions.begin(), potions.end());
        int m = potions.size();
        vector<int> ans;
        for (int& s : spells)
        {
            int left = 0, right = m;
            while (left < right)
            {
                int mid = (left + right) >> 1;
                if (1ll * s * potions[mid] >= success) right = mid;
                else left = mid + 1;
            }
            ans.push_back(m - left);
        }
        return ans;
    }
};
```

### **Go**

```go
func successfulPairs(spells []int, potions []int, success int64) []int {
	sort.Ints(potions)
	m := len(potions)
	var ans []int
	for _, s := range spells {
		left, right := 0, m
		for left < right {
			mid := (left + right) >> 1
			if int64(s*potions[mid]) >= success {
				right = mid
			} else {
				left = mid + 1
			}
		}
		ans = append(ans, m-left)
	}
	return ans
}
```

### **TypeScript**

```ts

```

### **...**

```

```

<!-- tabs:end -->
