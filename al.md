# Content
- [二分查找](#二分查找)

---
## 二分查找
- 前提: 有序, 数组
- 注意事项: 
  - 更新边界值时是否+-1
  - 终止条件: 比较边界值是否有等于
  - 取中值式: mid = left + (right - left) / 2, 原因: 防止相加溢出, 在负区间仍然向下取整
  - 区间: [a, b) , [a, b]
  - 是否有重复的值(见变体), 返回什么位置
- 变体: lower_bound, upper_bound

```
// [x, y)
int bsearch(int* A, int x, int y, int v) {
    int mid;
    while (x < y) {
        mid = x + (y - x) / 2;
        if (A[mid] == v)
            return mid;
        if (A[mid] > v)
            y = mid;
        else
            x = mid - 1;
    }
    return -1;
}
// [x, y]
int bsearch(int* A, int x, int y, int v) {
    int mid;
    while (x <= y) {
        mid = x + (y - x) / 2;
        if (A[mid] == v)
            return mid;
        if (A[mid] > v)
            y = mid - 1;
        else
            x = mid + 1;
    }
    reutrn -1;
}

// v in [lower_bound, upper_bound)
// lower_bound [x, y), 返回出现的第一个位置, 或是可以插入该值的位置
int lower_bound(int* A, int x, int y, int v) {
    int mid;
    while (x < y) {
        mid = x + (y - x) / 2;
        if (A[mid] >= v)
            y = mid;
        else
            x = mid + 1;
    }
    return x;
}
// upper_bound [x, y), 返回出现的最后一个位置的后一个位置, 或是可以插入的位置
int upper_bound(int* A, int x, int y, int v) {
    int mid;
    while (x < y) {
        mid = x + (y - x) / 2;
        if (A[mid] <= v)
            x = mid + 1;
        else 
            y = mid;
    }
    return x;
}
```
