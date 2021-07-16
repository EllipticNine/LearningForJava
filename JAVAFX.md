# JAVAFX

## 基本结构

### 一、舞台（Stage）

​	1、即：窗体，可包含场景

### 二、场景（Scone）

​	1、如：页面，可包含Node、Parent

### 三、Parent

​		1、Control（UI组件）

​		2、Pane（面板）

​	Nodes必须被包含在Parent组件中。

### 四、结点（Node）

​	包含：Shape（直线、圆、椭圆、矩形等）、ImageView

# 属性绑定

可以通过属性绑定将一个目标对象绑定到源对象中，源对象值一旦改变，目标对象值也相应改变。

` bind().divide(int div)`

# 结点通用属性

## 1、style（样式）

## 2、rotate（角度）

方法：contains(double x, double y);

# 常用类

##  一、Color类

`Javafx.scene.paint.Color`

```java
//Field
//三原色
double red;
double green;
double blue;
//透明度
double opacity;

//function
public Color(r,g,b,o);
Color brighter();
Color darker();
Color color(r,g,b);
Color color(r,g,b,o);
Color rgb(r,g,b);
Color rgb(r,g,b,o);
```

## 二、Font类

` javafx.scene.text.Font`

```java
//获取可用字体列表
List<String> getFamilies();
List<String> getFontNames();
//Field
double size;
String name;
String family;
//function
public Font(double size);
public Font(String name, double size);
public font(String name, double size);
public font(String name, FontWeight w, FontPosture p, double size);

```

## 三、Image 和 ImageView

​	` javafx.scene.image.Image`

​	 1、Image类表示一个图像

​	`javafx.scene.image.ImageView`

​	 2、ImageView表示用于显示图像

```java
//Field
ReadOnlyBooleanProperty error; //载入是否正确
ReadOnlyBooleanProperty height; //图像高度
ReadOnlyBooleanProperty width;  //图像宽度
ReadOnlyBooleanProperty progress; //图像载入百分比

Image image = new Image("file: ...URL");
                      OR http:  

```

