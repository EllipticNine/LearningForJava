# 异常处理和文本I/O

[ 要点 ]

1. 异常处理使得程序可以处理非预期的情景，并且继续正常的处理（若异常没有被处理，则程序会非正常终止）。
2. 异常是从方法抛出的。方法的调用者可以捕获以及处理该异常（利用throw抛出异常）。
3. 异常在程序中以“类”的形式存在，即：异常类。
4.  try{ } 模块中包含正常情况下执行的代码，异常被catch块捕获，并执行块中的代码以处理异常，执行完后执行后一条语句。
5. catch块的头部： catch ( ArithmeticException ex )
   1. ex 类似方法中的参数，ex之前的类型指定了catch块可以捕获的异常类型。
   2. 一旦捕获该异常，就能从catch中的参数访问这个抛出的值。

## 一、异常类型

根类：Throwable

### 1. 系统错误

由虚拟机抛出，用 ERROR 类表示，描述内部系统错误（让用户尽量稳妥终止程序）

​	例：LinkageError：一个类对另一个类有依赖性，但在编译前者后，后者进行了修改，变得不兼容。

​			VirtualMachineError：java虚拟机崩溃，或运行所必需的资源已经耗尽。



### 2. 异常

用 Exception 类表示，描述由程序和外部环境所引起的错误，这些错误能被程序捕获和处理

​	例：ClassNotFoundException：试图使用一个不存在的类

​			IOException：同输入输出相关的操作。如：无效输入、读文件时超过文件尾、打开一个不存在的文件等。

### 3. 运行时异常

由 RuntimeException 类表示，描述程序设计错误，如：错误的类型转换、越界数组、数值错误等，由JVM抛出

​	例：ArithmeticException：数学错误。如：除零。

​			NullPointerException：试图通过一个null引用变量访问对象。

​			IndexOutOfBoundException：数组下标超过范围。

​			IllegalArgumentException：传递给方法的参数非法。

### 免检异常：

### 	RuntimeException、Error以及它们的子类

### 必检异常：

其它异常都为必检异常，即：编译器强制程序员检查并通过try-catch块处理。

## 二、异常处理模型操作

### 过程

#### 1、声明一个异常

每个方法都必须声明它可能抛出的必检异常的类型

```java
public void myMethod() throws IOException, ... {}
```

#### 2、抛出一个异常

```java
IlligalArgumentException ex = new IlligalArgumentException("Wrong Argument");
throw ex;
//或
throw new IlligalArgumentException("Wrong Argument");
```

声明异常：throws

抛出异常：throw

#### 3、捕获一个异常

```java
try{
    ...
}
catch(Exception1 ex1){
    ...
}
catch(Exception2 ex2){
    ...
}
...
//未出现异常，不执行catch代码块
//出现异常，不执行try中剩余语句，而是沿方法调用链，反向寻找处理器
//    （判断异常类与catch中的异常块是否一致，一致则将异常对象赋值给所声名的变量）
//如果块可以捕获一父类的异常对象，则也可以捕获其所有的子类的异常对象
//
//多捕获特征简化异常
catch (Exception1 | Exception2 |...){
    
}
```



####  4、个别错误应当局部处理，以节省资源



#### 5、重新抛出异常

异常处理器不能处理一个异常，或只是简单的希望调用者注意到该异常，则允许重新抛出异常

```java
try{
    satement;
}
catch(TheException ex){
    perform operation before exits;
    throw ex;
}
```

#### 6、链式异常

main  -->  method1  --> method2 --> throw new Exception

主函数调用方法1,方法1调用方法2,方法二抛出异常给方法一，方法一处理包装该异常抛给主函数，主函数捕捉到该异常进行处理，打印追踪栈。



#### 7、创建自定义异常类

通过继承 java.lang.Exception 类





## 三、文本I/O

```java
File sourceFile = new File(String name);
Scanner input = new Scanner(sourceF);

```

实例化对象即可打开或创建文件或目录。

不论是否存在，都会在实例化过程中创建该文件或该目录。
