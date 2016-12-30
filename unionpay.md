# Content
- [定时任务](#定时任务)
- [性能测试](#性能测试)

## Notes
### 定时任务
- 使用quartz框架
- 目标: 互斥, 日志, 配置, 控制
- 使用数据库插入唯一记录是否成功保证互斥
- 使用模板模式, 搭建任务执行的上下文, 包括日志记录等
- 定时任务的入口, 实现`ServletContextListener`, 在`Listener`中实现

### 性能测试
- 测试分类:
  - 性能测试: 动力
  - 负载测试: 载重
  - 压力测试: 强度
- 指标:
  - 应用系统指标(LoadRunner, SoapUI, JMeter)
    - 并发数
    - 响应时间
    - 每秒初始事物数目(TPS吞吐量) TPS = 并发数 / 响应时间
    - 每秒返回字节数(Throughout吞吐率)
    - 每秒点击次数
    - 每秒成功点击次数
    - 每秒失败点击次数
  - JVM指标(JConsole, VisualVM, JProbe, JProfiler)
  - OS指标(nmon, vmstat)
    - CPU, MEM, IO, NET
