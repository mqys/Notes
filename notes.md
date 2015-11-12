## 随笔记录

记录零碎知识点

### c++虚函数表

<http://coolshell.cn/articles/12165.html>

对象内存的开始位置保存虚函数表，先父类后子类，若多继承，则有多个虚函数表。如果子类有重载父类函数，则表中的函数地址更新为子类函数的地址。

深入：c++内存模型：<http://coolshell.cn/articles/12176.html>

### c++: int to string

`to_string()`

### java 版本切换

更改JAVA_HOME环境变量的值即可 

``` 
export JAVA_7_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0.jdk/Contents/Home  
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home  
export JAVA_HOME=$JAVA_7_HOME  
```

