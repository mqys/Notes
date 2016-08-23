# Content
- [装配Bean](# 装配Bean)

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
  
  
