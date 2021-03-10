### 题目：回文数

给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。

回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。例如，121 是回文，而 123 不是。

示例 1：
```js
输入：x = 121
输出：true
```
示例 2：
```js
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```
示例 3：
```js
输入：x = 10
输出：false
解释：从右向左读, 为 01 。因此它不是一个回文数。
```
示例 4：
```js
输入：x = -101
输出：false
```

### 解题思路

1、字符串反转
```js
/**
 * @param {number} x
 * @return {boolean}
 */
function isPalindrome(x) {
  if (x < 0) return false
  return String(x).split('').reverse().join('') === String(x)
}
```

2、反转一半数字
```js
/**
 * @param {number} x
 * @return {boolean}
 */
 function isPalindrome(x) {
   if (x < 0 || (x !== 0 && x % 10 === 0)) return false
   var revertedNum = 0
   while (x > revertedNum) {
     revertedNum = (revertedNum * 10) + (x % 10)
     x = Math.floor(x / 10)
   }
   return x === revertedNum || x === Math.floor(revertedNum / 10)
 }
```

3、首尾二分对比
```js
/**
 * @param {number} x
 * @return {boolean}
 */
function isPalindrome(x) {
  let s = x.toString()
  let l = 0
  let r = s.length
  while (l < r) {
    if (str[l] !== str[r]) return false
    l++
    r--
  }
  return true
}
```