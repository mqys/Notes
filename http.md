# Content
- [HTTP基础](#HTTP基础)
  - [URL](#URL)
  - [HTTP报文](#HTTP报文)
  - [连接管理](#连接管理)
  
---
## HTTP基础
### URL
URL: 通过描述资源的位置来表示资源.

URN: 通过描述资源的名称来识别资源.

URL语法: 
```
<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
```
- <query>: 名/值对, 用`&`分隔

相对URL: 使用相对路径, 通过基础URL进行扩展, 组成新的绝对URL

字符限制: 需要对保留字符进行转义

### HTTP报文
报文组成: 起始行, 首部, 主体
- 每行以CRLF(回车+换行)结束
- 首部以一个空行结束

报文类型:
- 请求报文: 
```
<method> <request-URL> <version>
<headers>

<entity-body>
```
- 响应报文:
```
<version> <status> <reason-phrase>
<headers>

<entity-body>
```

- 起始行
  - <method>:
    - GET
    - HEAD: 在未获取资源的情况下, 对资源的首部进行检查. 返回的首部与GET返回的完全相同
    - POST(有body)
    - PUT(有body)
    - TRACE
    - OPTIONS: 请求web服务器告知其支持的各种功能
    - DELETE
  - <status>:
    - 100~199(信息性)
    - 200~299(成功): 200 OK
    - 300~399(重定向): 301 Moved Permanently, 302 Found
    - 400~499(客户端错误): 400 Bad Request, 401 Unauthorized, 403 Forbidden
    - 500~599(服务器错误): 500 Internal Server Error
- 首部
  - 通用首部: Connection, Date, MIME-Version, Via
  - 请求首部: Host, Accept
    - Accept
    - 条件请求首部: Except
    - 安全请求首部: Authorization, Cookie, Cookie2
    - 代理请求首部: Proxy-Authorization, Proxy-Connection
  - 响应首部: Age, Public, Server, Title
    - 协商首部: Accept-Range, Vary
    - 安全响应首部: Proxy-Authenticate, Set-Cookie, Set-Cookie2
  - 实体首部: Allow, Location
    - 内容首部: Content-Encoding, Content-Length, Content-Type
    - 实体缓存首部: ETag, Last-Modified
  - 扩展首部

### 连接管理
持久连接类型:
- HTTP/1.0+ "keep-alive"连接
  - Connection: Keep-Alive
  - 遇到哑代理失效
- HTTP/1.1 "persistent" 连接

关闭连接: 应该先关闭输出信道, 然后周期性地检查其输入信道的状态(查找数据, 或流的末尾)

