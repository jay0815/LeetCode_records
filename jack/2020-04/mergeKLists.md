### 23. 合并K个排序链表
> 合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:
```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```
---
#### 初始解题思路：
1. 通过将相邻链表合并，达到不开辟新空间的目的
2. 比较n-1次对全K个链表进行比较
#### 优化思路：
* 待思考补充

---
#### code

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
// 将k个序列分别两两合并并排序，最终合并成1组，完成排序
var mergeKLists = function(lists) {
    // 因为为限定lists是否可以为空，所以需要对边界进行处理
    if(lists.length === 0){
        return null
    }
    // 合并、排序
    const sort = (f, s) => {
        // 如果两两合并时，出现k为奇数个，f、s中参数可能为null
        // 如果出现链表迭代完全，则当前值也会为 null
        if(f === null){
            return s
        }
        if(s === null){
            return f
        }
        // 移动节点
        // 如果当前s值小于f,s.next与f比较,直到s.next大于当前f值
        // 或者完成s链表的迭代为止
        if(s.val <= f.val){
            s.next = sort(f, s.next)
            return s
        }else {
            f.next = sort(f.next, s)
            return f
        }
    }
    while(lists.length > 1){
        lists[1] = sort(lists[0], lists[1]);
        lists.shift();
    }
    return lists[0];
};
```
