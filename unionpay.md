# Content


## Notes
### 定时任务
- 使用quartz框架
- 目标: 互斥, 日志, 配置, 控制
- 使用数据库插入唯一记录是否成功保证互斥
- 使用模板模式, 搭建任务执行的上下文, 包括日志记录等