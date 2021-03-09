### 题目：计数质数

统计所有小于非负整数 n 的质数的数量。

示例 1：
```js
输入：n = 10
输出：4
解释：小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```
示例 2：
```js
输入：n = 0
输出：0
```
示例 3：
```js
输入：n = 1
输出：0
```

### 解题思路

#### 1、枚举

- 先判断是不是质数
  - 判断：质数是只能被`1`和`自身`整除的数
  - 范围：[2, $\sqrt{n}$]

- 再计算质数个数

```js
/**
 * @param {number} n
 * @return {number}
 */
function countPrimes(n) {
  // 创建一个临时数组，用于存储质数
  let res = []
  // 从2开始循环到n
  for (let i = 2; i < n; i++) {
    // 若i为质数
    if (isPrimes(i)) {
      // 则存放到数组中
      res.push(i)
    }
  }
  // 返回数组的个数
  return res.length
}
function isPrimes(num) {
  // 小于2的数不为质数
  if (num < 2) return false
  // 从 0 开始循环到 num的平方根 i
  for (let i = 2; i * i < x; i++) {
    // 若num能被i整除
    if (num % i === 0) {
      // 则不为质数
      return false
    }
  }
  // 若循环完，num不能被i整除，则为质数
  return true
}
```

#### 2、埃氏筛

- 质数的倍数是合数。`n`以内，从`2`起，顺序标记`质数`的倍数为`合数`
- 每找到一个质数，结果`+1`，返回结果

```js
/**
 * @param {number} n
 * @return {number}
 */
function countPrimes(n) {
  // 初始计数为0
  let count = 0
  // 把所有数都标记为质数(1)
  let isPrime = new Array(n).fill(1)
  // 从2开始循环到n
  for (let i = 2; i < n; i++) {
    // 若i为质数
    if (isPrime[i]) {
      // 计数加1
      count++
      // 循环质数i的倍数
      for (let j = i * i; j < n; j += i) {
        // 把质数i的倍数都标记为合数(0)
        isPrime[j] = 0
      }
    }
  }
  // 返回质数的计数
  return count
}
```

#### 3、线性筛
- 埃氏筛计算倍数为合数时，存在重复标记
- 两个质数的乘积，只可以组成一个合数
- 当前数能被质数数组中的`某质数`整除，当前数一定是包含`该质数`的合数

```js
/**
 * @param {number} n
 * @return {number}
 */
function countPrimes(n) {
  // 创建数组，存储质数
  let primes = []
  // 把所有数都标记为质数(1)
  let isPrimes = new Int8Array(n).fill(1)
  // 从2开始循环到n
  for (let i = 2; i < n; i++) {
    // 若i为质数
    if (isPrimes[i]) {
      // 存入质数数组中
      primes.push(i)
    }
    // 循环质数数组，且找到质数的倍数
    for (let j = 0, t; j < primes.length && (t = i * primes[j]) < n; j++) {
      // 把质数的倍数都标记为0
      isPrimes[t] = 0
      // 当前数能被质数数组中`某质数`整除，终止循环
      if (i % primes[j] === 0) break
    }
  }
  // 返回质数数组的个数
  return primes.length
}
```
