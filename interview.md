## notes on interview
  
---     
## 重载(overload), 重写(override)
- 重载(overload): 同名但参数不同的方法, 对返回值不做要求
- 重写(override): 子类对父类方法的重写, 形参/方法名/返回值都相同
  
## 锁
- 自旋锁(spinlock): 与互斥锁类似, 只有一个保持者, 不会睡眠, 轮询; 适用短时间持有锁的过程.
- RCU(Read-Copy Update): 对读操作不需要锁; 对写操作, 拷贝副本, 修改副本, 使用回调.
