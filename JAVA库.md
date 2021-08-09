# JAVA库

![java架构](C:\Users\EllipticNine\Desktop\MD\LearningForJava\java架构.png)

## 一、DATE类

###  ***+ Date(Elapse Time: long);***

Elapse Time : 流逝时间，即：从GMT时间（1970年1月1日8:00 am [东八区]）开始，经过（Elapse Time）毫秒(ms)的这一**时刻**。

### *+ ToString();*

返回代表时间和日期的字符串表示，即：将以毫秒为单位的时间转换为平常使用的时间和日期。

### *+ getTime();*

返回从GMT到目前为止的流逝的毫秒数。

### *+ setTime();*

在对象中设置一个新的流逝时间。

## 二、RANDOM类

### *+ Random();*

以当前时间为种子创建一个random对象。种子：是一个用于初始化一个随机数字生成器的数字。

### *+ Random(seed : long);*

以指定数字为种子，创建random对象。

### *+ nextInt() : int ;*

返回一个随机的int值。

### *+ nextInt(n : int) : int;*

返回一个0到n（不包含n）之间的随机一个整数。

### *+ nextLong() : long;*

返回一个随机的long值。

### *+ nextDouble() : double;*

返回0.0~1.0(不包含1.0)。

### *+ nextFloat() : float;*

返回0.0F~1.0F(不包含1.0F)。

### *+nextBoolean() : boolean;*

返回随机boolean值。





## 三、GregorianCalendar类

日历类，可同过get方法获取当前年、月、日。

用法：

```java
//实例化一个公历对象
GregorianCalendar ca = new GregorianCalendar();
ca.get(GregorianCalendar.YEAR);//获取年
ca.get(GregorianCalendar.MONTH);//获取月份（从0开始）
ca.get(GregorianCalendar.DAY_OF_MONTH);//获取日期
ca.setTimeInMillis(long); //设置从GMT时间开始流逝一定毫秒数后的一个特定时间
```



## 四、String类

- tips: String对象不可改变，字符串一经创建，内容不能再变。

### 1、构造字符串

```java
String newString = new String(stringLiteral); //通过构造函数传入字符串变量
```

或

```java
String newString = new String("Welcome to java"); //通过构造函数传入限定字符串
```

或

```java
String message = "Welcome to java"; //简写实例化，即：直接通过String关键字声明
```

或

```java
char[] charArray = {'G', 'o', 'o', 'd'};
String message = new String(charArray); //通过构造函数传入字符数组
```



- stringLiteral --------- 字符序列

  

### 2、不可变字符串与限定字符串

```java
String s1 = "Welcome to java";
String s2 = new String("Welcome to java");
String s3 = "Welcome to java";

//以上 s1 == s3 但 s1 != s2
//原因是JVM为节省效率，对相同字符序列的字符串直接量使用同一个实例
//s1和s2所指的实例不同，即：引用对象不同
```

### 3、字符串的替换和分隔

1. ``+replace(oldChar: char, newChar: char): String``

    将字符串中指定的a字符全部换成b字符。返回新字符串。

2. `` +replaceFirst(oldString: String, newString: String): String``

   将字符串中第一个匹配的子字符串替换成新的子字符串。返回新字符串。

3. `+replaceAll(oldString: String, newString: String): String`

   将字符串中所有匹配指定字符串的子字符串替换为新的子字符串。返回新字符串。

4. `+split(delimiter: String): String[]`

   传入指定分隔符，返回一个字符串数组，其中包含被分隔符分隔的子字符串集。

   

### 4、依照模式匹配、替换和分隔

​	正则表达式：

```java
String st;
st.matches("Java.*"); //以Java开头的子串
"440-12-123".matches("\\d{3}-\\d{2}-\\d{4}"); //  “\\d”表示单个数字位 “\\d{3}”表示三个数字位
```

​	正则表达式与replace、split结合使用：

```java
String s = "a+b$#c".replaceAll("[$+#]", "NNN"); // 用字符NNN替换$,+,#，返回一个新字符
String tokens = "JAVA, C?C#,C++".split("[.,:;?]"); //分隔字符串，分隔符为 . , : ; ?
```

### 5、字符串与数组之间的替换

​	_+toCharArray()_

​	_+getChar()_

例：	

```java
// 字符数组 ---> 字符串
char[] chars = "Java";
chars.toCharArray(); // 将字符数组“J，a，v，a”转化为字符串“Java”

char[] dst = {'J', 'A', 'V', 'A', '1', '3', '0', '1'};
"CS3720".getChar(2, 6, dst, 4); //将字符串 “CS3720” 下标 2 到 6-1 的子串 “3720” 复制到字符数组dst从下标4开始的位置

或
// 使用构造函数 String(char[]);直接构造
// 使用String.valueOf(new char[]{'2','3','4'});直接构造  
```

### 6、将字符和数值转换成字符串

```java
String valueOf(char c); //返回包含字符c的字符串
String valueOf(char[] data); //返回包含数组中字符的字符串
//返回表示相应值的字符串表述
String valueOf(double d);
String valueOf(float f);
String valueOf(int i);
String valueOf(long l);
String valueOf(boolean b);
```

### 7、格式化字符串

`String.format(format, item1, item2, ... , itemk);`

format -----> 格式

例：

```java
String s = String.format("%7.2f%6d%-4s", 45.556, 14, "AB");
//结果为
// XX45.56XXXX14ABXX
// X->代表空一格
```



## 五、StringBuilder 和 StringBuffer 类

「Notes」以上两类与String类的区别在于String类是不可改变的。

----------

StringBuilder 与StringBuffer的区别

​	StringBuilder适合 _单任务_ 访问，StringBuffer适合 _多任务_ 并发访问。两者的方法无明显区别，即：可替换。

------------

### 1、构造函数

```java
StringBuilder(); //构造容量为16的空字符串构建器
StringBuilder(int capacity); // 指定容量
StringBuilder(String s); //指定字符串
```

### 2、修改字符串

```java
//追加
StringBuilder append(char[] data); //追加字符数组到构建器中
StringBuilder append(char[] data, int offset, int len); //追加data中的子数组到构建器中
StringBuilder append(aPrimitiveType v); //将一个基本类型值作为字符串追加到构建器中
StringBuilder append(String s); //将追加一个字符串到构建器
//删除
StringBuilder delete(int startIndex, int endIndex); //删除从startIndex到endIndex-1的字符
StringBuilder deleteCharAt(int index); //删除指定索引位置的字符
//插入
StringBuilder insert(int index, char[] data, int offset, int len); //在指定的index位置插入data的子数组
StringBuilder insert(int offset, char[] data); //在偏移位置处插入数组
StringBuilder insert(int offset, aPrimitiveType b); //在偏移位置处插入一个转换为字符串的值
StringBuilder insert(int offset, String s); //在偏移位置处插入一个字符串
//替换
StringBuilder replace(int startIndex, int endIndex, String s); //从starIndex到endIndex-1的位置替换为给定字符串
//倒置
StringBuilder reverse(); //倒置字符，倒序排列
//修改
void setCharAt(int index, char ch); //修改指定索引位置的字符 
```



### 3、其它操作

```java
String toString(); //从构建器返回一个字符串对象
int capacity(); //返回构建器容量
char charAt(int index); //返回指定索引位置的字符
int length(); //返回存储的实际字符数
void setLength(int newLength); //设置新长度，若 > length则多余的位置追加空字符“\u0000”; 若 < length,则多的部分会被截断
String substring(int startIndex); //返回从startIndex开始的子字符串
String substring(int startIndex, int endIndex); //返回从startIndex到endIndex-1的子字符串
void trimToSize(); //减少存储大小,节省空间
```





## 六、ArrayList类

**[ Package ] : java.util.ArrayList**

### 1、asList();

静态方法

作用：从数组中创建一个数组列表

返回：一个列表

```java
String[] array = {"red", "blue", "yellow"};
ArrayList<String> list = new ArrayList<>(Array.asList(Array));
```

### 2、toArray( array );

作用：从一个数组列表来创建一个对象数组

传入：一个数组

结果：将ArrayList中的内容复制到 array 中

```java
String[] array1 = new String[list.size()];
list.toArray(array1);
```

### 3、sort();

**Package：java.util.Collections**

作用：排序

前提：列表中的元素是可比较的

```java
Integer[] array = {3, 5, 98, 4, 17, 34, 3, 5, 6};
ArrayList<Integer> list = new ArrayList<>(Arrays.asList(array));
java.util.Collections.sort(list);
```

### 4、max(); 和 min();

**[Package]: java.util.Collections**

作用：返回列表中最大和最小元素



### 5、shuffle();

静态

作用：随机打乱列表的元素





## 七、Throwable类

```java
import java.lang.Throwable;
```

### 1、getMessage()

返回描述该异常的对象的信息。

### 2、toString()

返回三个字符串的连接：异常类全名、": "、getMessage()

### 3、printStackTrace()

打印Throwable对象和它的调用堆栈信息。

### 4、getStackTrace()

返回和该异常对象相关的代表堆栈跟踪的一个堆栈跟踪元素的数组。





## 八、File 类

  [ 注 ] File类包含许多获取文件属性的方法，以及重命名和删除文件和目录的方法，但 “不包括” 读写文件内容的方法。

` java.io.File`

```java
File(String pathname); //为指定路径名（目录或文件）创建File对象
File(String parent, String child); //在parent目录下，创建一个子路径的File对象
File(File parent, String child); //在parent对象代表的目录下，创建一个子路径的File对象

exists();
canRead();
canWrite();
isDirectory();
isFile();
isAbsolute(); //对象采用绝对路径名创建，返回true
isHidden(); //对象代表的文件是隐藏的（即：系统相关），返回true

getAbsolutePath();
getCanonicalPath();
getName();
getPath();
getParent();

lastModified();
length();
listFile();
delete();
renameTo();
mkdir();
mkdirs();
```



## 九、文本I/O



### 写入文本：PrintWriter类

` java.io.PrintWriter;`

可以用来创建文件，并向其中写入数据。

```java
//创建文件对象
PrintWriter(File file);
PrintWriter(String filename);

//写入文件
print(String s);
print(char c);
print(char[] cArray);
print(int i);
print(long l);
print(float f);
print(double d);
print(boolean b);
```

使用 close() 方法关闭资源，正确保存。

可以使用 try-with-resources 来自动关闭资源

```java
try(PrintWriter output = new PrintWriter(file)){
    output.print("...");
}
```

资源创建放在小括号内，资源必须是AutoCloseable的子类。



### 读取文本： Scannner 类

```java
Scanner(File source);
Scanner(String source);
hasNext();
next();
...
Scanner useDelimeter(String pattern); //更改分隔符，返回该Scanner
```



### URL类

## 十、抽象类和接口

### 1、Number

#### Define

此类是Double, Float, Long, Integer, Short, Byte, BigInteger, BigDecimal类的抽象父类。





