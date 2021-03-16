### 快速排序

- 单边扫描
```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
function quickSort(nums) {
  sort(nums, 0, nums.length - 1)
  return nums
}
function sort(arr, left, right) {
  if (left < right) {
    let pivot = partition(arr, left, right)
    sort(arr, left, pivot - 1)
    sort(arr, pivot + 1, right)
  }
}
function partition(arr, left, right) {
  let pivot = arr[left]
  let mark = left
  for (let i = left + 1; i <= right; i++) {
    if (arr[i] < pivot) {
      mark++
      swap(arr, mark, i)
    }
  }
  swap(arr, left, mark)
  return mark
}
function swap(arr, i, j) {
  let temp = arr[i]
  arr[i] = arr[j]
  arr[j] = temp
}
```

