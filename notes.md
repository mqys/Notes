## 随笔记录
记录零碎知识点

### java 版本切换
更改JAVA_HOME环境变量的值即可 
``` 
export JAVA_7_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0.jdk/Contents/Home  
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home  
export JAVA_HOME=$JAVA_7_HOME  
```

### CMake使用
创建临时文件夹用来放编译的过程文件
```
mkdir build
cd bulid
cmake ..
make
```



  
