## 准备

### 1、安装

gem install sass

### 2、把sass编译为css

sass sass/style.scss:css/style.css

### 3、自动编译

sass --watch sass:css 自动观察sass目录并输出到css目录

### 4、修改编译输出的css格式

sass --watch sass:css --style nested|compact|expanded|compressed

nested：嵌套， 默认是这种格式

compact：紧凑

expanded: 扩展

compressed: 压缩

### 5、.sass与.scss的区别

.sass采用的是缩进式语法、.scss与我们常写的css语法基本相似

![image-20200905190459474](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905190459474.png)

## 基础

### 1、变量

![image-20200905201511601](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905201511601.png)

### 2、嵌套

![image-20200905201800254](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905201800254.png)

### 3、嵌套式引用父选择器

![image-20200905202056931](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905202056931.png)

### 4、属性嵌套

![image-20200905202654886](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905202654886.png)

### 5、混合mixin

![image-20200905203102325](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905203102325.png)

### 6、mixin里面的参数

![image-20200905203533102](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905203533102.png)

### 7、继承/扩展

![image-20200905203906308](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905203906308.png)

### 8、partials与@import

@import扩展了css的@import，文件名必须以_开头，不会被sass编译为单独的css文件。

![image-20200905204332370](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905204332370.png)

### 9、注释

![image-20200905204659629](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905204659629.png)

## 数据类型

### 1、数据类型date type

使用type-of(5)可以查看数据类型。主要有：number、string、list、color四种类型数据

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905214859132.png" alt="image-20200905214859132" style="zoom:67%;" />

### 2、数字运算

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200905215257297.png" alt="image-20200905215257297" style="zoom:67%;" />

### 3、数组函数

abs()绝对值、round()四舍五入、ceil()向后进一位、floor()取整、percentage()百分比、min(1, 2, 3)最小数、max(1, 2, 3)最大数

![image-20200906010539189](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906010539189.png)

### 4、字符串

字符串操作“+”、“-”、“、”  “*”不认识，会报错

![image-20200906011009238](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906011009238.png)

### 5、字符串函数

To-upper-case 、to-lower-case 、str-length、Str-index、Str-insert

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906011408310.png" alt="image-20200906011408310" style="zoom:67%;" />

### 5、color表示方式

字符串：green、blue、red   

RGB形式：rgb(0, 0, 0)

hsl(0, 100%, 50%)

### 6、rgb与rgba

rgb(红,绿,蓝)

### 7、hsl与hsla

### 8、adjust-bue

![image-20200906012728580](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906012728580.png)

### 9、lighten与darken

![image-20200906013038240](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906013038240.png)

### 10、ssaturate和desaturate

![image-20200906013528074](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906013528074.png)

### 11、opacify和transparentize

### 12、列表-list

### 13、列表函数

![image-20200906100522576](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906100522576.png)

### 14、map与相关函数

### 15、布尔值

### 16、interpolation

![image-20200906101615223](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906101615223.png)

## 控制指令

### 1、控制指令-control Directives

### 2、@if

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906102036826.png" alt="image-20200906102036826" style="zoom:67%;" />

### 3、@for

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906102443608.png" alt="image-20200906102443608" style="zoom:67%;" />

### 4、@each

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906102743654.png" alt="image-20200906102743654" style="zoom:50%;" />

### 5、@while

<img src="/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906103547275.png" alt="image-20200906103547275" style="zoom:50%;" />

## 自定义

### 1、用户自定义函数

![image-20200906103955446](/Users/fuaoqi/Library/Application Support/typora-user-images/image-20200906103955446.png)

### 2、警告与错误