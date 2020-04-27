### 33. 搜索旋转排序数组
> 假设按照升序排序的数组在预先未知的某个点上进行了旋转。
( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。
搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。
你可以假设数组中不存在重复的元素。
你的算法时间复杂度必须是 O(log n) 级别。

示例 1:
```javascript
输入: nums = [4,5,6,7,0,1,2], target = 0
```

输出: 4
示例 2:
```javascript
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```
---
#### 解题思路：
1. 假设按照升序排序的数组在预先未知的某个点上进行了旋转。 === 节点都是升序的，但是存在分段
2. 搜索步骤
    - 确认分段范围
    - 根据待搜索的数值大小，确认搜索分段
    - 根据搜索值确认搜索方向
```javascript
var search = function(nums, target) {
    // 方案一 indexOf 在LeetCode已有用例中，比我在后面实现的二分查找性能要好😢
    return nums.indexOf(target)
    // 方案2
    // 搜索分段值：第一段的最大值和第二段的最小值，确认分段值的索引范围
    // let middle = 0;
    // // 二分查找 分段值 和对应的索引
    // let start = 0, end = nums.length - 1;
    // while(start <= end){
    //     middle = start + ((end - start) >> 1);
    //     if(nums[middle] === target){
    //         return middle
    //     }
    //     // 递增数据的旋转后特征：范围内递增
    //     // 当前 start -> middle 是属于同递增段
    //     if(nums[middle] >= nums[start]){
    //         // target 在 start -> middle 范围内，改变end，继续二分搜索
    //         if(target >= nums[start] && target <= nums[middle]){
    //             end = middle - 1;
    //         }else {
    //             // target 在 middle -> end 范围内，改变start，继续二分搜索
    //             start = middle + 1;
    //         }
    //     }else {
    //         // 当前 middle -> end 是属于同递增段
    //         // target 在 middle -> end 范围内，改变start，继续二分搜索
    //         if(target >= nums[middle] && target <= nums[end]){
    //             start = middle + 1;
    //         }else {
    //             // target 在 start -> middle 范围内，改变end，继续二分搜索
    //             end = middle - 1;
    //         }
    //     }
    // }
    // // 处理循环跑完找不到
    // return -1;
};
```
