### 题目：主要元素

数组中占比超过一半的元素称之为主要元素。给定一个整数数组，找到它的主要元素。若没有，返回-1。

示例 1：
```js
输入：[1,2,5,9,5,9,5,5,5]
输出：5
```

示例 2：
```js
输入：[3,2]
输出：-1
```

示例 3：
```js
输入：[2,2,1,1,1,2,2]
输出：2
```

### 解题思路
1、摩尔投票法
- 比拼消耗
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
function majorityElement(nums) {
  let major
  let count = 0
  for (let i = 0; i < nums.length; i++) {
    if (count === 0) {
      major = nums[i]
      count++
    } else {
      if (major === nums[i]) {
        count++
      } else {
        count--
      }
    }
  }
  if (count > 0) {
    let t = 0
    for (let n in nums) {
      if (nums[n] === major) t++
      if (t > Math.floor(nums.length / 2)) return major
    }
  }
  return -1
}
```

