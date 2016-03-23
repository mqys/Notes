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

#include <unistd.h>
int close(int sockfd); // close sockfd -> send FIN
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

---
## I/O复用
