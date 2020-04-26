### 20. 给定一个只包括 '('，')'，'{'，'}'，'['，']'  的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例:

```javascript
输入: "()[]{}";
输出: true;
输入: "(]";
输出: false;
```

---

```javascript
var isValid = function (s) {
  if (s.length === 0) return true;
  if (s.length % 2 !== 0) return false;

  const disc = {
    "}": "{",
    "]": "[",
    ")": "(",
  };

  const stack = [];

  for (let i = 0, j = s.length; i < j; i++) {
    const curChar = s[i];
    const lastChar = stack[stack.length - 1];
    const delChar = disc[curChar];

    if (delChar) {
      if (delChar === lastChar) {
        stack.pop();
      } else {
        return false;
      }
    } else {
      stack.push(delChar);
    }
    return !s.length;
  }
};
```
