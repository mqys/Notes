# Building high performance web

## Chapter 12 - Web 负载均衡
### HTTP重定向
- 302 + 使用响应头中的`Location`

### 负载策略
- Round Robin(轮询): 需要缓存保存计数, 开销很大, 计数访问的原子性限制并发量
- 带权重的RR
- 随机调度
- 根据用户ip散列

### DNS

### 反向代理
- http层, 七层负载均衡
- 黏滞会话(Sticky Sessions): 让用户的一次会话周期内的所有请求始终转发到一台特定的后端服务器上
  - 使用IP进行Hash
  - 追加服务器信息到Cookie

### IP负载均衡: NAT

## Chapter 18 - 性能监控
### 实时监控
- Nmon

### 监控代理
- SNMP服务

### 系统监控
- Cacti

### 服务监控
- Apache mod_status
