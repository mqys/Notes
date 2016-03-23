# Content
- I/O: 不带缓冲的I/O, 文件和目录, 标准I/O, 高级I/O(多路转接, 异步), 终端I/O 
- 进程: 进程环境, 进程控制, 进程关系, 信号, 线程, 线程控制, 守护进程, IPC, 网络IPC(套接字)

## 线程同步
- 互斥量:
    - 对同一互斥量加锁两次则死锁(不可重入)

```
int pthread_mutex_init(pthread_mutex_t *restrict mutex, contst pthread_mutexattr_t *restrict attr);
int pthread_mutex_destroy(pthread_mutex_t *mutex);

int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
int pthread_mutex_unlock(pthread_mutex_t *mutex);                        
```
- 读写锁:

```
int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_unlock(pthread_rwlock_t *rwlock);
```
- 条件变量

## 进程间通信
- 管道
- FIFO
- 消息队列
- 信号量
- 共享存储
- 套接字