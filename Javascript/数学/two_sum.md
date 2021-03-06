### 题目：两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

你可以按任意顺序返回答案。

示例 1：
```js
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```
示例 2：
```js
输入：nums = [3,2,4], target = 6
输出：[1,2]
```
示例 3：
```js
输入：nums = [3,3], target = 6
输出：[0,1]
```

### 解题思路

1、 双重循环

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
function twoSum(nums, target) {
  // 循环当前数组
  for (let i = 0; i < nums.length; i++) {
    // 从当前值开始，循环数组中剩余内容
    for (let j = i + 1; j < nums.length; j++) {
      // 若两值相加等于目标值
      if (nums[i] + nums[j] === target) {
        // 返回对应下标
        return [i, j]
      }
    }
  }
}
```

2、Map
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
function twoSum(nums, target) {
  // 创建一个Map
  const map = new Map()
  // 循环当前数组
  for (let i = 0; i < nums.length; i++) {
    // 获取目标值与当前值的差值
    const num2 = target - nums[i]
    // 若Map中存在差值
    if (map.has(num2)) {
      // 返回差值坐标和当前值坐标
      return [map.get(num2), i]
    }
    // 若Map中不存在差值，则存入该差值坐标
    map.set(num2, i)
  }
}
```
