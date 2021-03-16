### 题目：字符串相乘

给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

示例 1:
```js
输入: num1 = "2", num2 = "3"
输出: "6"
```
示例 2:
```js
输入: num1 = "123", num2 = "456"
输出: "56088"
```
说明：

num1 和 num2 的长度小于110。
num1 和 num2 只包含数字 0-9。
num1 和 num2 均不以零开头，除非是数字 0 本身。
不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。

### 解题思路

- 乘数`num1`位数为M，乘数`num2`位数为N，两数相乘，结果最大总位数为M+N
- `num1[i] * num2[j]`的结果为两位数，第一位是`arr[i+j]`，第二位是`arr[i+j+1]`

```js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */

 function multiplyString(num1, num2) {
   if (num1 === '0' || num2 === '0') return '0'
   let len1 = num1.length
   let len2 = num2.length
   // 定义一个最大总位数的数组，填满0
   let arr = new Array(len1 + len2).fill(0)
   // 从num1末尾循环
   for (let i = len1 - 1; i >= 0; i--) {
     // 从num2末尾循环
     for (let j = len2 - 1; j >= 0; j--) {
       let sum = num1[i] * num2[j] + arr[i+j+1]
       arr[i+j+1] = sum % 10
       arr[i+j] = Math.floor(sum / 10) + arr[i+j]
     }
   }
   // 若首位为0，则去除
   if (arr[0] === 0) arr.shift()
   return arr.join('')
 }
```