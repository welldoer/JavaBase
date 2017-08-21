## 【类和字节码】

### 类加载和类对象
- 一个.class　文件定义了JVM中的类型，包括了域,方法，继承信息，注解和其他元数据

#### 加载和连接
![图](https://raw.githubusercontent.com/Kuangcp/ImageRepos/master/Tech/Book/Java7Developer/p107.jpg)

`加载`
- 这个过程就是读取字节码文件，创建一个字节数组装在这些内容，加载结束后这个对象还不能直接调用 

`连接`
- 加载完成后，类必须连接起来，分为三步：验证，准备，解析。
    - 验证：
        - 验证文件的合理性，完整性检查，检查常量池，方法的字节码检查。主要的：
        - 是否所有方法都遵守访问控制关键字的限定
        - 方法调用的参数个数和静态类型是否正确
        - 确保字节码不会试图滥用堆栈
        - 确保变量使用之前被正确初始化了
        - 检查变量是否仅被赋予恰当类型的值
    - 准备：
        - 分配内存，准备初始化类中的静态变量，但不会现在就初始化，也不会执行任何VM字节码
    - 解析：
        - 促使VM检查类文件中所引用的类型是不是都是已知的类型。如果有运行时有未知的类型，那又要引发一次类加载过程
        - 当需要加载的类全部加载解析完毕后，VM就可以初始化最初那个加载的类了。
        - 这时所有的静态变量都可以进行初始化，所有静态代码块都会运行，这一步完成后，类就能使用了
        
#### Class对象
- 加载和连接过程的最终结果是一个Class对象，Class对象可以和反射API一起实现对方法，域构造方法等类成员的间接访问

#### 类加载器
![图](https://raw.githubusercontent.com/Kuangcp/ImageRepos/master/Tech/Book/Java7Developer/p110.jpg)

- Java平台经典类加载器：
    - 根（引导）加载器： 通常在VM启动后不久就实例化，作用是加载系统的基础JAR(主要是rt.jar)，并且不做验证工作
    - 扩展类加载器： 加载安装时自带的标准扩展，一般包括安全性扩展
    - 应用或系统类加载器： 应用最广泛的类加载器，负责加载应用类，在大多SE环境中主要工作是由他完成
    - 定制类载器： 为了企业框架定制的加载器
    
### 方法句柄
> 主要用于反射 用到再学

![图](https://raw.githubusercontent.com/Kuangcp/ImageRepos/master/Tech/Book/Java7Developer/p118.jpg)


### 检查类文件
#### javap
> 用来探视类文件内部和反汇编文件

### 常量池
> 常量池是为类文件中的其他常量元素提供快捷访问方式的区域。对于JVM来说常量池相当于符号表
> [参考博客](http://www.cnblogs.com/LeonNew/p/5314731.html)

- `javap -v class文件` 输出很多额外信息，# 开头的就是常量池信息
![图](https://raw.githubusercontent.com/Kuangcp/ImageRepos/master/Tech/Book/Java7Developer/p120.jpg)

### 字节码

- 字节码是程序的中间表达形式，源码和机器码之间的产物
- 字节码是由源文件执行javac产生的
- 某些高级语言特性（语法糖）在字节码中给去掉了，例如循环结构，会转换成为分支指令
- 每个操作都由一个字节表示，因此叫做字节码
- 字节码是一种抽象表示方法
- 字节码进一步编译得到机器码

- `javap -c -p class文件` 反编译字节码文件，-p 能看到私有属性
    - 输出所有的属性以及类的定义信息
    - 静态块
    - 构造方法
    - 方法信息
    - 静态属性信息
    - 静态方法信息

#### 运行时环境
> 因为JVM没有CPU那样的寄存器，所以是采用的堆栈来计算的，称为操作数栈或者计算堆栈

- 当一个类被链接进运行时环境时，字节码会受到检查，其中很多验证都可以归结为对栈中类型模式的分析
- 方法需要一块内存区域作为计算堆栈来计算新值，另外每个运行的线程都需要一个调用堆栈来记录当前正在执行的方法，这两个栈会有交互

#### 操作码介绍
- 字节码由操作码 opcode 序列构成，每个指令后可能会带参数，操作码希望看到栈处于指定状态中，然后他对栈进行操作处理，把参数移走，放入结果
- 操作码表有四列：
    - 名称：操作码类型的通用名称
    - 参数：操作码的参数，以i开头的是用来作为常量池或局部变量中的查询索引的几个字节，如果有更多的参数，将会合并
        - 如果参数出现在括号里，就表明不是所有形式的操作码都会使用他
    - 堆栈布局：他展示了栈在操作码执行前后的状态。括号中的元素表示是可选的
    - 描述：描述操作码的用处

#### 加载和存储操作码
#### 数学运算操作码
#### 执行控制操作码
#### 调用操作码
#### 平台操作码
#### 操作码的快捷形式
#### invokedynamic
> 这个特性是针对 框架开发和非Java语言准备的



    
    
    