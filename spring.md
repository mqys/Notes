# Content
- [装配Bean](# 装配Bean)
- [事务管理](# 事物管理)

## 装配Bean
### 装配机制 (自动 > java > xml)
- 在xml中显式配置
  - 在xml文件中使用<bean>标签: id, class;
  - <constructor-arg>标签: value, ref, list, set
- 在java中显式配置
  - 在配置类中, 添加`@Bean`的标签, 定义对象生成的方式的函数
- 隐式的bean发现机制和自动装配
  - 实现类: `@Component`
  - 配置类: `@Configuration`, `@ComponentScan`(默认是本包下)
    - `@ComponentScan(basePackages={"soundsystem", "video"})`, `@ComponentScan(basePackagesClasses={CDPlayer.class, DVDPlayer.class})`(类型安全)
  - 装配类: `@RunWith(SpringJUnit4ClassRunner.class)`, `@ContextConfiguration(classes=CDPalyerConfig.class)`' ,`@Autowired` 
    - 有且只有一个bean匹配依赖需求的时候, 这个bean才会被装配进来
- 默认情况下, spring中的bean都是单例的
- 配置混合使用: 
  - 在javaconfig中引用其他: `@Import(CDconfig.class)`, `@ImportResource("classpath:cd-config.xml")`
  - 在xml引用其他: `<bean class="soundsystem.CDConfig">`, `<import resource="cdplayer-config.xml">`
  
## 事务管理
- 传播行为: 何时创建一个事务或者何时使用已有的事务

| 传播行为 | 含义 | 
| --- | --- |
| PROPAGATION_MANDATORY | 该方法必须在事务中运行, 若事物不存在则抛出异常 | 
| PROPAGATION_NESTED | 如果当前已经存在一个事务, 则在嵌套事务中执行 | 
| PROPAGATION_NEVER | . |
| PROPAGATION_NOT_SUPPORTED | 不应该在事务中 | 
| PROPAGATION_REQUIRED | 必须在事务中运行, 若事物不存在则创建新的事务 |
| PROPAGATION_REQUIRED_NEW | 必须运行在自己的事务中 | 
| PROPAGATION_SUPPORTS | 不需要事务上下文, 如果存在当前事务的话, 就在事务中运行 |

- 隔离级别: 一个事务被其他并行的事务所能影响的程度
  - 并发问题:
    - 脏读: 一个事务读取另一个事务改写但未提交的数据, 随后改写被回滚了
    - 不可重复读: 一个事务执行相同的查询, 每次的结果不同. (值-更新)
    - 幻读: 一个事务多次读取几行数据的查询, 发现了原本不存在的一些记录. (数目-插入)

| 隔离级别 | 含义 | 
| --- | --- |
| ISOLATION_DEFAULT | 默认 |
| ISOLATION_READ_UNCOMMITTED | 允许读取尚未提交的数据, 可能出现脏读, 不可重复读和幻读 | 
| ISOLATION_READ_COMMITED | 允许读取并发事务已提交的数据, 阻止脏读, 可能不可重复读和幻读 | 
| ISOLATION_REPEATABLE_READ | 对同一字段多次读取结果一致, 除非数据是本事务所修改. 阻止脏读和不可重复读, 可能幻读 |
| ISOLATION_SERIALIZABLE | ACID, 阻止脏读/不可重复读/幻读 |

- 是否只读
- 事务超时
- 回滚规则
