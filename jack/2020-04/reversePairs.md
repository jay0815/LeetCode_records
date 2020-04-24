### 面试题51. 数组中的逆序对

> 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

* 如果使用暴力法(挨个比较),需要时间复杂度为 n^2
* 此处使用归并排序法，因为每次排序完成后，排序的对象总是从小到大。所以比较相同位置上的数值时，可以很快得出，比当前较小的数据大一侧的数据的数量 时间复杂度为 nlog(n)

>>拆分处理
>>>* 拆分开始
>>>* 第1次拆分 [2,7,8] [9,1,1,2] =>
>>>* 第2次拆分
{[2,7], [8]}
{[9,1], [1,2]}
>>>* 拆分完成

```flow
st=>start: 开始拆分
en=>end: 结束拆分
cond=>condition: Array.length < 2 ?
op=>operation: splice Array
st->cond
op->en
cond(true)->en
cond(false)->op
```
>>比较
>>>* 比较开始
>>>* left: [2,7] right: [8] =>
>>>* 2 < 8  =>
>>>* left.shift() & left: [7] right:[8] merge: [2]
>>>* 7 < 8  =>
>>>* left.shift() & left: [] right:[8] merge: [2, 7]
>>>* left[0] === undefined 循环结束
>>>* right剩余 此时 8 大于 2、7 (结论：剩下的数据，一定都至少大于等于 merge 中的数据)
>>>* merge.concat(right)
>>>* 回溯继续比较

```flow
st=>start: 开始比较
en=>end: 结束比较
while=>condition: left[0] or right[0] equals undefined
if=>condition: left[0] > right[0]
rp=>operation: shift right and count left length
lp=>operation: shift left
adlm=>operation: push left head item into merge
adrm=>operation: push right head item into merge
mg=>operation: left or right 合并到merge上
st->while
while(true)->mg
while(false)->if
if(true)->adrm->rp->while
if(false)->adlm->lp->while
mg->en
```
```javascript
var reversePairs = function(nums) {
    let sum = 0;
    const compare = (nums) => {
        // 控制最小拆解的比较对象为长度为1或0的数组
        if(nums.length < 2) return nums;
        // 二分数组
        const middle = Math.floor(nums.length/2);
        // 递归记录
        return mergeAndCount(compare(nums.slice(0, middle)), compare(nums.slice(middle)))
    }
    const mergeAndCount = (left, right) => {
        // 用于记录当前归并比较后的数据，小的在左，大的在右
        const merge = [];
        // 当left数组与右数组中有一方被完全出栈时，停止循环
        while(left[0] !== void 0 && right[0] !== void 0){
            // 条件为左数大于右数时，那么当前左数所满足逆序对的数量为当前left的长度
            if(left[0] > right[0]){
                sum+= left.length;
                // 将值较小的数放入按照从小到大排序的merge中去
                merge.push(right[0]);
                // right出栈，将下一个待比较的right 数据移至第一位
                right.shift();
            }else {
                // 左侧数小于右侧数
                merge.push(left[0]);
                // left出栈，将下一个待比较的left数据移至第一位
                left.shift();
            }
        }
        // left未比较完，将剩余数据合并到merge上
        if(left.length > 0){
            merge.push(...left)
        }
        // right未比较完，将剩余数据合并到merge上
        if(right.length > 0){
            merge.push(...right)
        }
        return merge;
    }
    compare(nums)
    return sum
};
```

[https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)
