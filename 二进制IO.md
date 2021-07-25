# 一、基本概念

## （一）文本文件与二进制文件区别

​	1、文本文件可以使用文本编辑器进行处理（读取、创建、修改）。

​	2、二进制文件是所有非文本文件，不能使用文本编辑器进行处理。

​	3、文本文件是由“字符”序列构成，二进制文件是由位（bit）序列构成。

​	4、二进制文件处理效率高于文本文件。

## （二）Java如何处理文本I/O

​	1、使用Scanner类读取文本数据。

​	2、使用PrintWriter类写文本数据。

## （三）文本I/O与二进制I/O

​	1、二进制I/O不涉及编码与解码，因此比文本I/O效率更高。

​	2、读写二进制文件的根类：

​		（1）InputStream

​		（2）OutputStream

```mermaid
classDiagram
	Object <|-- InputStream
	Object <|-- OutputStream
	class InputStream{
		+read() int
		+read(byte[] b) int
		+read(byte[] b, int off, int len) int
		+available() int
		+close() void
		+skip(long n) long
		+markSupported() boolean
		+mark(int readlimit) void
		+reset() void
	}
	class OutputStream{
		+write(int b) void
		+write(byte[] b) void
		+write(byte[] b, int off, int len) void
		+close() void
		+flush() void
	}
	class FileInputStream{
		+FileInputStream(File file) void
		+FileInputStream(String filename) 
	}
	InputStream <|-- FileInputStream
	InputStream <|-- FilterInputStream
	InputStream <|-- ObjectInputStream
	FilterInputStream <|-- DataInputStream
	FilterInputStream <|-- BufferedInputStream
	OutputStream <|-- FileOutputStream
	OutputStream <|-- FilterOutputStream
	OutputStream <|-- ObjectOutputStream
	FilterOutputStream <|-- DataOutputStream
	FilterOutputStream <|-- BufferedOutputStream
		
```

