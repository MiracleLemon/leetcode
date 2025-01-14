# [93. 复原 IP 地址](https://leetcode.cn/problems/restore-ip-addresses)

[English Version](/solution/0000-0099/0093.Restore%20IP%20Addresses/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p><strong>有效 IP 地址</strong> 正好由四个整数（每个整数位于 <code>0</code> 到 <code>255</code> 之间组成，且不能含有前导 <code>0</code>），整数之间用 <code>'.'</code> 分隔。</p>

<ul>
	<li>例如：<code>"0.1.2.201"</code> 和<code> "192.168.1.1"</code> 是 <strong>有效</strong> IP 地址，但是 <code>"0.011.255.245"</code>、<code>"192.168.1.312"</code> 和 <code>"192.168@1.1"</code> 是 <strong>无效</strong> IP 地址。</li>
</ul>

<p>给定一个只包含数字的字符串 <code>s</code> ，用以表示一个 IP 地址，返回所有可能的<strong>有效 IP 地址</strong>，这些地址可以通过在 <code>s</code> 中插入&nbsp;<code>'.'</code> 来形成。你 <strong>不能</strong>&nbsp;重新排序或删除 <code>s</code> 中的任何数字。你可以按 <strong>任何</strong> 顺序返回答案。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "25525511135"
<strong>输出：</strong>["255.255.11.135","255.255.111.35"]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "0000"
<strong>输出：</strong>["0.0.0.0"]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = "101023"
<strong>输出：</strong>["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 20</code></li>
	<li><code>s</code> 仅由数字组成</li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

DFS。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        def check(s):
            if not (0 <= int(s) <= 255):
                return False
            if s[0] == '0' and len(s) > 1:
                return False
            return True

        def dfs(s, t):
            if len(t) == 4:
                if not s:
                    ans.append('.'.join(t))
                return
            for i in range(1, min(4, len(s) + 1)):
                if check(s[:i]):
                    t.append(s[:i])
                    dfs(s[i:], t)
                    t.pop()

        ans = []
        dfs(s, [])
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    private List<String> ans;

    public List<String> restoreIpAddresses(String s) {
        ans = new ArrayList<>();
        dfs(s, new ArrayList<>());
        return ans;
    }

    private void dfs(String s, List<String> t) {
        if (t.size() == 4) {
            if ("".equals(s)) {
                ans.add(String.join(".", t));
            }
            return;
        }
        for (int i = 1; i < Math.min(4, s.length() + 1); ++i) {
            String c = s.substring(0, i);
            if (check(c)) {
                t.add(c);
                dfs(s.substring(i), t);
                t.remove(t.size() - 1);
            }
        }
    }

    private boolean check(String s) {
        if ("".equals(s)) {
            return false;
        }
        int num = Integer.parseInt(s);
        if (num > 255) {
            return false;
        }
        if (s.charAt(0) == '0' && s.length() > 1) {
            return false;
        }
        return true;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> ans;
        vector<string> t;
        dfs(s, t, ans);
        return ans;
    }

    void dfs(string s, vector<string>& t, vector<string>& ans) {
        if (t.size() == 4) {
            if (s == "") {
                string p = "";
                for (auto e : t) p += e + ".";
                p.pop_back();
                ans.push_back(p);
            }
            return;
        }
        for (int i = 1; i < min(4, (int) s.size() + 1); ++i) {
            string c = s.substr(0, i);
            if (check(c)) {
                t.push_back(c);
                dfs(s.substr(i, s.size() - i), t, ans);
                t.pop_back();
            }
        }
    }

    bool check(string s) {
        if (s == "") return false;
        int num = stoi(s);
        if (num > 255) return false;
        if (s[0] == '0' && s.size() > 1) return false;
        return true;
    }
};
```

### **Go**

```go
func restoreIpAddresses(s string) []string {
	check := func(s string) bool {
		if i, _ := strconv.Atoi(s); i > 255 {
			return false
		}
		if s[0] == '0' && len(s) > 1 {
			return false
		}
		return true
	}
	var ans []string
	var dfs func(s string, t []string)
	dfs = func(s string, t []string) {
		if len(t) == 4 {
			if s == "" {
				ans = append(ans, strings.Join(t, "."))
			}
			return
		}
		for i := 1; i < 4 && i < len(s)+1; i++ {
			if check(s[0:i]) {
				t = append(t, s[0:i])
				dfs(s[i:], t)
				t = t[0 : len(t)-1]
			}
		}
	}
	var t []string
	dfs(s, t)
	return ans
}
```

### **...**

```

```

<!-- tabs:end -->
