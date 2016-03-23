## 基本套接字
```
#include <sys/socket.h>
struct sockaddr {
 uint8_t        sa_len;
 sa_family_t    sa_family;
 char           sa_data[14];   
};

#include <netinet/in.h>
struct in_addr {
    in_addr_t   s_addr;
};
struct sockaddr_in {
    uint8           sin_len;
    sa_family_t     sin_family;
    in_port_t       sin_port;
    struct in_addr  sin_addr;
    char            sin_zero[8];  
};
```

```
#include <sys/socket.h>
int socket(int family, int type, int protocol); // 返回非负描述符
// family: AF_INET, AF_INET6 ...
// type: SOCK_STREAM, SOCK_DGRAM ...
// protocol: IPPROTO_TCP, IPPROTO_UDP ...

int connect(int sockfd, const struct sockaddr *servaddr, socklen_t addrlen);

int bind(int sockfd, const struct sockaddr *myaddr, socklen_t addrlen);
 
int listen(int sockfd, int backlog); 

int accept(int sockfd, struct sockaddr *cliaddr, socklen_t addrlen); // 返回非负描述符

// UDP
ssize_t recvfrom(int sockfd, void *buff, size_t nbytes, int flags, struct sockaddr *from, socklen_t *addrlen);
ssize_t sendto(int sockfd, void *buff, size_t nbytes, int flags, struct sockaddr *to, socklen_t *addrlen);

int shutdown(int sockfd, int howto);
// howto: SHUT_RD 关闭读, SHUT_WR 关闭写, SHUT_RDWR 读写都关

#include <unistd.h>
int close(int sockfd); // close sockfd -> send FIN
// close将描述符的引用计数减一, 仅在计数为0的时候关闭套接字
// close终止读写两个方向的数据传送
```

```
// 字节操纵函数
#include <strings.h>
void bzero(void *dest, size_t nbytes);
void bcopy(const void *src, void *dest, size_t nbytes);
int bcmp(const void *ptr1, const void *ptr2, size_t nbytes);

#include <string.h>
void *memset(void *dest, int c, size_t len);
void *memcpy(void *dest, const void *src, size_t nbytes);
int memcmp(const void *ptr1, const void *ptr2, size_t nbytes);
```

给UDP增加可靠性:
- 相比TCP缺少: 正面确认, 丢失分组重传, 排序; 窗口流量控制; 慢启动和拥塞避免;
- 增加序列号和时间戳: 超时和重传, 序列号 

---
## I/O复用
I/O模型:
- 阻塞式I/O
- 非阻塞式I/O (轮询)
- I/O复用 (select / poll)
- 信号驱动式I/O (SIGIO)
- 异步I/O

```
#include <sys/select.h>
#include <sys/time.h>
struct timeval {
  long tv_sec;  // seconds
  long tv_usec; // microseconds 
};

void FD_ZERO(fd_set *fdset);
void FD_SET(int fd, fd_set *fdset);
void FD_CLR(int fd, fd_set *fdset);
int FD_ISSET(itn fd, fd_set *fdset);

int select(int maxfdp1, fd_set *readset, fd_set *writeset, fd_set *exceptset, const struct timeval *timeout);
// timeout: NULL -> 一直等待,直到有描述符准备好; timeval -> 不为0,等待一段时间 / 为0, 轮询

int pselect(int maxfdp1, fd_set *readset, fd_set *writeset, fd_set *exceptset, const struct timespec *timeout , const sigset_t *sigmask);
// struct timespec使用纳秒级别
// 多信号掩码, 允许程序先禁止一些信号的传递

#include <poll.h>
struct pollfd {
    int     fd;
    short   events;     // 测试事件
    short   revents;    // 返回状态
};
int poll(struct pollfd *fdarray, unsigned long nfds, int timeout);

```
