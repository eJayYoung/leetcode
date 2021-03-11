### 题目：二进制求和

给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 非空 字符串且只包含数字 1 和 0。

示例 1:
```js
输入: a = "11", b = "1"
输出: "100"
```
示例 2:
```js
输入: a = "1010", b = "1011"
输出: "10101"
```

### 解题思路

1、利用`BigInt`进行相加计算，`toString`返回二进制数
```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
function addBinary(a, b) {
  const result = BigInt('0b' + a) + BigInt('0b' + b)
  return result.toString(2)
}
```

2、补位对齐，从末尾逐位相加得进位与和
```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
 function addBinary(a, b) {
   // 定义ans保存和拼接的字符串
   let ans = ''
   // 定义进位变量
   let carry = 0
   // 两个字符串从右往左循环
   for (let i = a.length - 1, j = b.length - 1; i >= 0 || j >= 0; i--, j--) {
     // 定义当前对位之和
     let sum = carry
     // 若当前字符存在，则转为数字相加，不存在，则补位为0
     sum += i >= 0 ? parseInt(a[i]) : 0
     sum += j >= 0 ? parseInt(b[j]) : 0
     // 对位之和除2的余数从左往右拼接，组成逆序的合（不含进位）
     ans += sum % 2
     // 计算当前对位之和的进位
     carry = Math.floor(sum / 2)
   }
   // 最后进位为1，则拼接
   ans += carry == 1 ? carry : ''
   // 将逆序的和的字符串反转
   return ans.split('').reverse().join('')
 }
```
