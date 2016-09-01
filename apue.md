# Content
- I/O: 不带缓冲的I/O, 文件和目录, 标准I/O, 高级I/O(多路转接, 异步), 终端I/O 
- 进程: 进程环境, 进程控制, 进程关系, 信号, 线程, 线程控制, 守护进程, IPC, 网络IPC(套接字)

## 文件I/O
```
#include <fcntl.h>
int open(const char*pathname, int oflag, ... /*mode_t mode*/);
// oflag: O_REONLY, O_WRONLY, O_RDWR
//        O_APPEND, O_CREAT, O_EXCL .....

int create(const char*pathname, mode_t mode);

#include <unistd.h>
int close(int filedes);

off_t lseek(int filedes, off_t offfset, int whence);
// whence: SEEK_SET(设置偏移量), SEEK_CUR(当前值加上offset), SEEK_END(文件长度加上offset)
//        offset可正可负

ssize_t read(int filedes, void *buf, size_t nbytes); 
// 成功返回读到的字节数

ssize_t write(int filedes, void *buf, size_t nbytes);
// 成功返回已写的字节数

int dup(int filedes);
int dup2(int filedes, int filedes2);
// 复制文件描述符, 返回新的文件描述符
    
```

## 进程
- 孤儿进程和僵尸进程
  - 孤儿进程: 父进程结束, 子进程还在运行, 这些子进程将成为孤儿进程. 孤儿进程将被init(1)进程回收;
  - 僵尸进程: 子进程退出, 而父进程未调用`wait`或者`waitpid`来获取子进程状态信息, 子进程的进程描述符仍在系统中; 大量僵尸进程将导致系统不能创建新的进程.

```
#include <unistd.h>
pid_t fork(void);
// 子进程返回0, 父进程返回子进程ID

#include <sys/wait.h>
pid_t wait(int *statloc);
pid_t waitpid(pid_t pid, int *statloc, int options);
// 一个进程终止时, 内核向其父进程发送SIGCHLD信号
// pid: -1 -> 等待任一子进程

#include <unistd.h>
int execl(const char *pathname, const char *arg0, ... /*(char *) 0 */);
int execv(const char *pathname, const char* arg[]);
// execle, execve, execlp, execvp
// l->list, v->vector, e->environment, p->PATH(从环境变量中寻找可执行文件)

```

## 线程
```
#include <phtread.h>
int pthread_create(pthread_t *restrict tidp, const pthread_attr_t *restrict attr, void *(*start_rtn)(void*), void *restrict arg);

void pthread_exit(void *rval_ptr);

int pthread_join(pthread_t thread, void **rval_ptr);

int pthread_cancel(pthread_t tid);
// 请求取消同一进程中的其他线程

int pthread_detach(pthread_t tid); 
```

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
