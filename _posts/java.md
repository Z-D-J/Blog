---
title: java
date: 2020-09-11 16:39:07
tags:

---

# 输入和输出

* 使用`Scanner in = new Scanner(System.in);`可以定义一个可以接受输入的东西`in`（名字是任取的。）。之后要接受输入时，就使用形如`in.nextline()``in.nextint()`的语句。（其中line与int表示接受的输入的数据类型，line是字符串，int是整型）。
* 使用` System.out.println();`可以直接输出字符串并且在每一次输出后都换行，还有`System.out.print()`，它与前者的区别是在每一次输出后不换行。
* `System.out.prinf()`这个输出的用法与c语言中的printf()类似，可以有`System.out.printf("%.2f",i)`这样的类似c语言的格式限制。
* Java的注释和c语言一样，可以用`//`和`/**/`，还有`/** */`用来为注释javadoc标明。
# 变量

* 变量的定义：<类型名称> <变量名>;
* 变量的名字(又叫做标识符）只能由字母，数字和下划线组成，且数字不可以出现在第一个位置上。Java的内置的关键字不可以用作变量名。
* Java是一种强类型语言，变量在使用前必须声明，且变量具有确定的类型。
* 所有被声明的变量都是有默认值的。例如：数字类型的默认值为0,引用类型的默认值为null，布尔值为false。不过方法中局部变量声明后不会进行默认的初始化,所以必须进行明确初始化。

# 常量

* 类似变量的定义声明，常量只需要在定义时在类型前加上关键词`final`。常量只能在定义时赋值初始化，之后不能再赋值。
* 可以在类中定义final类型的实例字段。如果在定义时没有给final类型的变量赋值，那么就可以在**构造器**（也只有在构造器中，其他方法不行）中为它赋值
* **变量的作用域**：总的来说，Java中变量的作用域就是在它被定义的花括号之内。如，在for循环内部定义的就只在该循环内有效，在函数内部定义的就只在函数内部有效。

# 运算

## 赋值

* 同c语言一样，Java依旧使用`=`来进行赋值。
* 在定义变量的时候可以进行赋值（此时叫做变量的初始化）。
* 赋值运算是自右向左。

### 复合赋值

* 同c语言一样，Java中也有复合赋值，即`+=, -=, *=, /=`。用法与c语言完全一致。`a += b + c`与`a = a + (b + c)`完全相同。

## 四则运算
  
* 当浮点数和整数放在一起运算时，Java会将整数先转化为浮点数，之后进行浮点数的运算。
* `+，-，*,/ , %`的运算优先级和惯常的优先级一致。特别的，`%`对于小数也可以使用。
* 赋值号`=`的优先级很低，以保持和正常思维一样的运算顺序。
* Java中同样有`i++, ++i`这种运算，用法与c语言完全相同。

## 位运算

* 为运算是用来处理整型数据的。
* 位运算符包括`&(and), |(or), ^(xor), ~(not)，>>, <<, >>>`.
* `&, |, ^, ~`是对每一位进行和，或，异或，非的运算。
* `>>,<<`是将位左移或者右移。`>>`用符号位填充高位。
* `>>>`进行左移，但是用0来填充高位。

## 单目运算符

* 取正`+`和取负`-`,运算优先级高于普通的双目运算符。


# 数据类型

## 整型

* 整数类型不能表达有小数部分的数。整数与整数的运算结果还是整数。
* Java中所有的数字都是有符号的，没有无符号类型。
* `int`型：

## 浮点型

* 浮点数就是通常所说的小数。
* `double`型的浮点数：

## 布尔类型

* Java中的布尔类型是用`boolean`定义的，其含义与用法与c语言中的bool类型一致。但是整型与boolean是严格区分的，即将boolean类型变量赋为0或者1是不行的。

## 字符类型

* 单个字符类型是char，其字符字面量是用单引号来表示的，如'a','4'等。Java中的字符使用的是Unicode标准，支持汉字在内的多种文字。
* 类似C语言中的字符类型，可以对字符变量进行加减运算。如`i = 'A' - 'D'`中的i为3，也可以强制将字符类型转换为int类型。
* **逃逸字符**：有些没有办法打印出来的字符，这些字符由一个反斜杠`\`开头，后面跟上一个字符，由这两个字符合起来组成一个字符。常见逃逸字符：

|字符|意义|
|-|-|
|\b|回退一格|
|\t|到下一个表格位|
|\n|换行|
|\r|回车|
|\"|双引号|
|\'|单引号|
|`\\`|反斜杠本身|


## 包裹类型

* 每种基础类型（如，int，double，char）都有对应的包裹类型。
* 包裹类型除了具有和基础类型一样的功能外（如定义变量），还有许多可以实现的功能。如`Integer.MAX_VALUE`,可以得到int类型的最大值。即使用包裹类型可以调用许多java内置的方法。
* 包裹类型的第一个字母是大写的。
* 各种基础类型对应的包裹类型。

|基础类型|包裹类型|
|-|-|
|int|Integer|
|double|Double|
|char|Character|
|boolean|Boolean|

## 字符串变量

* **字符串字面量**：用双引号括起来的0或者多个字符为一个字符串字面量。如："hello"
* **字符串类型**：`String`是字符串类型（第一个字母为大写，是一种包裹类型），String是一个类，String类型的变量是字符串的管理者而非所有者（就和数组变量和数组一样。）
* **字符串变量的创建**：
  * 法一：`String s = new String(字符串字面量)`.用字符串字面量初始化字符串变量。也可以直接初始化一个字面量，如`String s = "hello"`。
  * 法二：使用`StringBuider <字符串名> = new StringBuilder();`可以创建一个空的字符串(但是这样创建的不是String类型，而是StringBuilder类型的变量了，使用`<字符串名>.append(ch)`或者<字符串名>.append(str)`来给字符串追加内容。(更多方法请查阅java.lang.StringBuilder)                                                              
* **字符串的连接**：使用`+`可以将两个字符串连接起来，如果`+`两边的不是字符串类型，它会自动将非字符串类型的转为字符串类型。
* **字符串的读入**：使用`in.nextline()`能直接读入一个字符串，字符串之间以回车为表示。（使用`in.next()`可以读入单词，每个单词之间用空格隔开。）
* 字符串是只读的变量，不可以通过赋值来修改。
* **String[]**代表的是**字符串数组**，即一个元素类型为String类型的数组。注意与String类型的区分。

### 字符串的操作

* 字符串的数据是对象，可以通过`.`这个操作来实现对字符串的操作。
* **字符串的比较**：`s.compareTo(s1)`;
* **获得字符串的长度**：`s.length()`;
* **访问字符串中的单个字符**：`s.charAt(3)`.(3是字符的索引，类似数组，但不可直接像访问数组中元素一样使用a[i]这样的访问)。
* **判断两个字符串是否相同**：`s.equal(s1)`.
* **获得字符串的子串**：`s.substring(2,4)`或者`s.substring(2)`,括号中是字符的索引，单独的2代表从索引为2以后开始的子串，但是（2，4）代表从索引为2字符以后开始，到索引为4字符之前。
* **寻找字符串中的字符**：`s.indexOf(c)`或者`s.indexOf(c,n)`或者`s.indexOf(s1)`。括号中只有字符c代表找到字符串中c字符所在位置的索引。（c，n）表示从n位置开始寻找c字符，s1为字符串变量，（s1）能找到字符串s1所在的位置。还可以从右边开始找`s.lastIndexOf(同普通的)`.
## 强制类型转换

* Java同c语言一样，有很多隐式转换。例如整型在某些条件下会自动转为浮点型。
* 但是浮点型不会自动转换为整型。我们可以进行强制类型转换。例如：`int a = (int)(32 /5 .0)`。

## var声明局部变量

* 当变量的类型可以从它的初始值中推导出来时，可以使用var关键字来声明，而无需指明其类型。如：`Employee harry = new Employee();`可以写作`var harry = new Employee();`。
* var关键字只能用于方法中的局部变量，**参数和实例字段**的类型必须明确声明。

# 关系运算

* 关系运算符：`==, >, <, >=, <=, !=`与C语言一致。
* 关系运算符的优先级比算术运算符低，但是比赋值运算高。例如：`7 > 3 + 2`。
* 判等和判不等`==, !=`的优先级比`<, <=, >, >=`低.例如：`5 > 3 == 6 > 4`是可行的（但是和c语言一样，尽量不要连续使用关系运算。）
* `<, >, >=, <=`是不能连续使用的，例如：`a > b > c`是和你的想象完全不同的。

## 浮点数的比较

* 整型是可以与浮点数进行比较的。
* 浮点数的运算有误差。所以判断两个浮点数是否相等是用`Math.abs(a -b) < 1e-6`.先用`Math.abs(a - b)`算出两个浮点数之间的差值，在让这个差值和一个很小的数比较。`1e-6`表示的是1的负6次方。


# 控制语句

## 条件语句

### if语句  

* 与c语言类似，只有一个语句时可以不用花括号（但是建议不管多少语句都用花括号），但是有多条语句时必须括起来。
* 类似c语言，Java中的if语句同样可以与else连用，进行级联条件判断。

### swich语句

* Java中同样有switcl-case语句。用法也与c语言相同。
* 示例：
```java
switch (控制表达式) {
    case 常量：
        语句
        ...
        break;
    case 常量：
        语句
        ...
        break；
    ...
    default:
        语句
        ...
        break;
}
```
* 控制表达式，只能是整型的结果；
* 每个case后面都要有**break**语句。
* 如果所有的case都不匹配，就执行default后面的语句；如果没有设置default语句，就什么也不做。(default后面直接接冒号，没有条件。default后面的语句也可以放break来终止。）

## 循环语句

### while

* 与c语言中的while基本一致。 while是当条件满足时执行循环内的语句。
* 与c语言一样，Java中也有`do-while`循环，这个循环至少执行一次。do-while循环是一直执行直到while语句中的条件**不满足**。

### for循环

* Java中也有for循环，用法与c语言基本相似。
* 但是Java可以在循环条件语句中定义变量，并且在for循环中定义的变量只能在for循环中使用，在循环体外并没有那个变量的定义。例如：`for(int i =  1; i <= n; i = i + 1 ){}`。（for循环适合有明确结束条件的循环。）
* `break`语句在Java中与c语言中一致，用于跳出循环。
* `continue`语句也是与c语言一样，用于到达循环尾。(但是continue语句不会跳过for循环的步进语句，例如：`for(int i = 0; i <= n; i++){continue;}`， 每次continue语句之后还是要执行i++之后再开启下一轮循环。)。
* **循环的标号**：可以在循环前设置一个标号（例如;`out:`）来标示循环。使用`break  标号`和`continue 标号`可以使break和continue对标号标示的循环起作用。示例：
```java
OUt:
for(int i = 0; i <= n1; i++){
    for(int j = 0; j <= n2; j++){
        break OUT;
    }
}
```
OUT标示的循环是最外层的循环，使用`break OUT`能直接跳出最外层的循环。
* **for-each**循环：形如:`for (int i : numbers){}`,意思是每一次循环，一次将数组numbers中的元素值赋给变量i。常用于遍历数组（foreach循环不能用于遍历字符串，即java中字符串与数组没有c语言中那么亲密的关系）。 示例：
```java
int[] numbers = new int[100];

// 依次遍历数组中每个元素，并在数组遍历完之后停止循环。
for (int i : numbers) {
    if (i == 23) {
        System.out.println("numbers数组中有23这个数")；
        break；
    }
}

```
# 逻辑类型

* 关系运算的结果是一个逻辑值，true或者false。这个值保存在一个对应的逻辑类型的变量中，这个类型是boolean。与c语言的布尔类型一样，Java中的布尔类型也只有true和false这两种值。

## 逻辑运算

* **!**:逻辑非。
* **&&**：逻辑与。
* **||**：逻辑或。三者都与c语言中的逻辑运算的用法一致。

# 数组

* 数组定义：形如`int[] numbers = new int[100]`。格式范式：`<类型>[] <名字> = new <类型>[元素个数]`（同c语言一样，数组的下标是从0开始的，后面方括号中是数组中元素的个数(可以为变量，但是必须有）。但是实际只有numbers[99], 而没有numbers[100].)
* 数组一旦创建，不能被改变大小。
* 数组中的所有元素是同一类型。
* java中的每个数组有一个内部成员length,这个变量中存储了数组中元素的个数（即创建数组时确定的元素个数）。使用示例；
```java
int[] numbers = new int[100];

for(int i = 0; i < numbers.length; i++) {
    ...
}
```
* 数组的直接初始化：形如：`int[] numbers = {1, 2, 3, 4, 5};`
* 数组变量之间可以做赋值。例如：`int[] numbers = {1, 2, 3, 4, 5}; int[] b = numbers;`.数组变量的实质与c语言类似，是指向实际存储空间的“指针”，但是Java中不使用指针的概念，可以把数组变量看作是实际存储空间的管理者。所以数组变量之间的赋值，其实质是将对实际存储空间的管理权共享了出去，而不是把整个数组复制过去。因此，如果改变了b数组中，某个元素的值，numbers数组中相应的元素也会跟着改变。如`b [2] = 3;`之后会有`numbers[2] == 3`.
* **拷贝**数组元素到另一个数组中：`var a = new X[list.size]; list.toArray(a)`。将list数组的元素拷贝到a数组中去。（适用于各种类型的数组，包括泛型数组列表）
* 对数组对象的操作需要使用**Arrays**类中的方法。
* main函数必须带的参数`String[] args`是main函数接收命令行参数的字符串类型的数组。
* 数组变量之间的比较，是在比较两个数组变量是否管理同一个数组，而不是比较两个数组是否是每个元素都对应相等。
* 刚创建的int类型数组，数组中的元素默认都是0。
* **二维数组**：定义形如`int[][] numbers = new int[3][5];`;与c语言类似，通常理解为矩阵。二维数组初始化：
```java

int[][] numbers = {
    {1, 2, 3, 4}, //每一行用逗号，分隔。
    {5, 6, 7}, //第二行比第一行少了一个元素，编译器会自动补上0；
};//别忘了最后的分号。
```
* 二维数组中仍然有length变量表示数组的长度。`numbers.length`表示数组的的行数。而每一行有多少个元素需要用`numbers[i].length`。


# Math类

* Math类提供的很多数学操作，如取绝对值等。
* `abs`提供取绝对值操作，`.round`提供四舍五入的操作，`.random`提供取随机数（0到1之间）的操作，`.pow`可以进行幂运算。
* 使用示例：
```java

Math.abs(-12); //结果为12
Math.round(10.2343); //结果为10
Math.random(); 
Math.pow(2, 3); //结果为2的3次方：8
```

# 函数

## 函数定义

* 函数可以接收0个或者多个参数，做一件事，并返回0个或者一个值。
* 函数定义：函数头（函数名，返回类型，参数表），函数体。函数定义示例：
```java
public static boolean sum(int a, int b) 
{
    ...
    return true;  
}
```
## 函数调用

* 函数调用格式：`函数名（参数）`,注意，即使函数不需要参数，也需要括号。
* 函数可能会有返回值，此时需要有对应的变量来接收返回值。void类型的函数是没有返回值的。
* 传递给函数的参数类型要匹配，如果类型不匹配，则在某些情况下函数会自动转换。（条件是函数需要的类型比实际传进来的参数类型“宽”，如double类型比int类型宽。）。
* 传递给函数的参数，实际是传的值，即没有传进去变量本身，而只是变量值的一个副本。在函数内部是无法修改传进来的参数的值的。

## 函数的本地变量

* 同c语言一样，Java函数内部定义的变量在函数外部是不可见的。函数内部定义的本地变量，只在函数内部有效。


# 类与对象

## 类与对象的基本定义

* **类**：定义同一类事物，Java中所有的代码都位于某个类里。（类的第一个字母要大写）类定义示例：
```java
public class Hero {
     
    String name; //姓名
     
    float hp; //血量
     
    float armor; //护甲
     
    int moveSpeed; //移动速度
}
```
* **对象**：类就像是一个模板，根据这个模板可以创建很多同一类的东西，这些根据类创建出来的东西就是对象。由类构造对象的过程叫做**实例化**。对象创建示例:
```java
public class Hero {
     
    String name; //姓名
     
    float hp; //血量
     
    float armor; //护甲
     
    int moveSpeed; //移动速度
     
    public static void main(String[] args) {
        Hero garen =  new Hero(); //对象的创建类似于数组或者String类型的变量的创建。
        garen.name = "盖伦";
        garen.hp = 616.28f;
        garen.armor = 27.536f;
        garen.moveSpeed = 350;
         
        Hero teemo =  new Hero();
        teemo.name = "提莫";
        teemo.hp = 383f;
        teemo.armor = 14f;
        teemo.moveSpeed = 330;
    }  
     
} //英雄是一个大类，而具体的每个英雄则是一个对象
``` 
* **属性**：类中定义的变量就是类的属性(类中的数据又叫做**实例字段**），类中的属性就像一种东西的各种属性。属性可以是基本类型（如int等）也可以是**类类型**（如String等）.属性名称一般是小写，但是如果由两个及以上单词组成，则从第二个单词开始，首字母大写。
  * 类中的实例字段只能由自己类中的方法来直接访问。
  * 所有对象的实例字段描述了对象当前状况的信息，这就是对象的**状态**。
*  **方法**：类中的东西不仅具有属性，它还会做事情，能做的事情就是类中的方法。（方法的实质是在类中定义的函数）.方法的命名方法与属性一样。方法与属性的调用方法都是通过在对象后使用`.`。
   *  通常的类没有main方法，却有自己的实例字段和方法。要想构建一个完成的程序，会使用多个类，但是**只有一个类有main方法**。
*  示例：
```java
public class Hero {
    String name; //姓名
      
    float hp; //血量
      
    float armor; //护甲
      
    int moveSpeed; //移动速度
 
    //Hero方法:坑队友
    void keng(){
        System.out.println("坑队友！");
    }
}
```

## 对象变量

* 不是基本类型而是类类型的变量，又叫做**对象变量**，对象变量可以用来引用该类的对象。
* 对象的创建时用`new Hero()`,但是创建的对象需要一个变量来接收才能使用，于是`Hero h = new Hero()`，此时的`=`不再是对于基本类型的赋值的意思，而是**指向**的意思。这个Hero类型的变量h就又叫做引用。（用c语言指针的概念来理解：就是h指向刚创建的Hero对象，但是Java中没有指针这个概念，所以只是一种理解）
* 对象变量可以**赋值**，如`Date deadline = birthday`(birthday也是一个对象变量，现在这两个对象变量引用同一个对象)。对象变量可以赋值为**null**，代表这个对象变量当前没有引用任何对象。
* 对象变量的值除了用new操作符，使用构造器获得外，还可以调用返回对象的引用的方法来赋值。如`DayOfWeek weekday = date.getDayOfWeek();
* 根据引用的概念，对象的创建又可以写为：
```java
public class Hero {
      
    String name; //姓名
      
    float hp; //血量
      
    float armor; //护甲
      
    int moveSpeed; //移动速度
      
    public static void main(String[] args) {
        //创建一个对象,但是没有引用。
        new Hero();
         
        //使用一个引用来指向这个对象
        Hero h = new Hero();
         
    }  
      
}
```
* （类比c语言的指针），可以有多个引用指向同一个对象，但是一个引用不能同时指向多个对象。

## 继承

* 如果另一类东西有已经定义的某一类东西全部属性，则可以通过继承来避免属性的重复定义。
* 继承是一种`is-a`关系，即子类包含于父类中，子类的特性（字段和方法）**更多**。例如：人类是一个父类，而男人可以作为人类的一个子类。
* 父类又称为：超类、基类；子类又称为：派生类、孩子类。
* 子类从父类那里继承了**方法**和**字段**（如果是在父类中用private修饰的**私有字段**和**私有方法**（大多数时候是私有字段），即使是子类也**无法访问**）。
* 根据对象的多态性，可以将**子类对象赋给父类引用变量**，但是反之不行。因为如果将父类对象赋给子类的引用变量，如果这个变量调用子类特有的方法就会出错。但是父类中的方法，子类对象都具有，所以不会出错。
* 继承是通过关键字`extends`来实现的。示例：
```java
public class Item {
    String name;
    int price;
}

// 非继承的写法，武器是一种物品。
public class Weapon{
    String name;
    int price;
    int damage; //攻击力
 
}
//继承的写法

public class Weapon extends Item{ // 通过extends来实现继承
    int damage; //攻击力
     
    public static void main(String[] args) {
        Weapon infinityEdge = new Weapon();
        infinityEdge.damage = 65; //damage属性在类Weapon中新设计的
         
        infinityEdge.name = "无尽之刃";//name属性，是从Item中继承来的，就不需要重复设计了
        infinityEdge.price = 3600;
         
    }
     
}
```

### 方法覆盖（重写）

* 父类中的某些方法可能对子类不适用，此时就需要在子类中重新写一个**名字相同但是实现不同**的方法。

### super

* super关键字可以在子类中调用父类的方法。
* super关键字可以在子类中调用父类的构造器。如`super(name,salry)`。具体调用父类的哪个构造器是由参数的数目和类型决定的。
* 另外，经常是在子类的构造器中调用父类的构造器来节省部分代码，但是**super调用构造器的语句只能作为子类构造器的第一个语句**出现。

### 继承层次

* 由一个公共父类派生出来的所有类的集合称为**继承层次**。
* 在继承层次中从某个特定的类到其祖先的路径称为该类的**继承链**。

### 阻止继承：final类与方法

* 被声明为final的类，是不能被继承的。声明格式`public final class Hello {...}`。
* 方法也可以被声明为final，这代表这个方法不能在子类中被**覆盖（重写）**。final类中的所有方法都被自动声明为final类型的方法（但是不会将字段自动变为final类型）。
* 字段被声明为final类型就与继承没有关系。final字段是指，该字段在对象构造出来之后就不能被修改了。

### 对象引用的强制类型转换

* 在继承层次内才能进行对象引用的强制类型转换。
* 只能将父类强制类型转换为子类，并且应该使用instanceof检查要转换的两个类型之间是否为父子类关系。
* 示例：`boss = (Manger) staff[1]`。

### 对象包装器与自动装箱

* 所有的基本类型都有一个与之对应的类。（如：Integer类对应基本类型int）。这些类称为**包装器**。
* 包装器有：`Integer, Long, Float, Double, Short, Byte, Character, Boolean`。
* 包装器是**不可变**的类，包装器被构造之后，就不允许更改包装在其中的值。包装器是**final**类型的类，不能派生子类。
* 包装器的用途：将基本类型如int转换为对象。如：ArrayList<Integer>`。因为尖括号中必须是普通的类，所以不能使用int，此时可以用Integer达到相同的效果。
* **自动装箱**：在声明为包装器类的地方使用对应的基本类型，会自动将该基本类型的元素转换为对应的包装器类，这种特性叫做自动装箱。如：`list.add(3)`将自动转换成`list.add(Integer.valueOf(3))`。
* **自动拆箱**：在声明为基本类型的地方使用对应的包装器类，会自动将该包装器类的元素转换为对应的基本类型。
* 包装器中还有很多基本静态方法。如`int x = Integer.parseInt(s)`可以将s字符串转换为整型数值。 

### 参数数量可变的方法

* 示例：`public PrintStream printf(String fmt, Object...args)`。其中`...`是java代码的一部分。，表明这个方法可以接收任意数量的对象。实际上这个方法接收两个参数，一个是格式字符串fmt，一个是`Object[]`数组。`Object[]`数组中保存着其它所有参数。

### 反射

* 暂时略。

## 方法重载

* 方法重载指的是**方法名一样，但是参数不一样**。每次调用该名字的方法时，会自动根据对应的参数类型以及数量来调用对应的方法。示例：
```java
public class ADHero extends Hero {
    public void attack() {
        System.out.println(name + " 进行了一次攻击 ，但是不确定打中谁了");
    }
 
    public void attack(Hero h1) {
        System.out.println(name + "对" + h1.name + "进行了一次攻击 ");
    }
 
    public void attack(Hero h1, Hero h2) {
        System.out.println(name + "同时对" + h1.name + "和" + h2.name + "进行了攻击 ");
    }
 //可以给类似的方法设置同样的名字。
    public static void main(String[] args) {
        ADHero bh = new ADHero();
        bh.name = "赏金猎人";
 
        Hero h1 = new Hero();
        h1.name = "盖伦";
        Hero h2 = new Hero();
        h2.name = "提莫";
 
        bh.attack(h1);
        bh.attack(h1, h2);
    }
 
}
```
* 方法重载还可以通过设置可变数量的参数来实现。可变数量的参数通过数组来实现。示例：
```java
public class ADHero extends Hero {
 
    public void attack() {
        System.out.println(name + " 进行了一次攻击 ，但是不确定打中谁了");
    }
 
    // 可变数量的参数
    public void attack(Hero... heros) { //方法的形参需要设置...<数组名>来表示这个函数是接受可变参数的
        for (int i = 0; i < heros.length; i++) {
            System.out.println(name + " 攻击了 " + heros[i].name);//数组设置的参数调用方法与普通数组一样。
 
        }
    }
 
    public static void main(String[] args) {
        ADHero bh = new ADHero();
        bh.name = "赏金猎人";
 
        Hero h1 = new Hero();
        h1.name = "盖伦";
        Hero h2 = new Hero();
        h2.name = "提莫";
 
        bh.attack(h1);
        bh.attack(h1, h2);
 
    }
 
}
```
## 构造方法

* 实例化：通过一个类创建一个对象的过程叫做实例化。
* **构造方法（构造器）**：实例化是通过调用构造方法来实现的。构造方法同其他方法一样具有一样具有参数和语句体，但是没有返回类型。构造方法不是成员方法，不能用对象来调用它。**构造方法的名字与类的名字一样**，包括大小写也一样。
* 每个类可以有一个以上的构造器。
* **不要**在构造方法（类中的其它方法也一样）中使用与实例字段同名的局部变量。
* 示例：
```java
public class Hero {
 
    String name;
 
    float hp;
 
    float armor;
 
    int moveSpeed;
 
    // 方法名和类名一样（包括大小写）
    // 没有返回类型
    public Hero() {
        System.out.println("实例化一个对象的时候，必然调用构造方法");
    }
     
    public static void main(String[] args) {
        //实例化一个对象的时候，必然调用构造方法
        Hero h = new Hero();//new 后面跟的是构造方法，只是构造方法的名字与类的名字是相同的。
    }
}
```
* 如果在定义类中没有对构造方法的定义，则编译器在编译时会自动给类加上一个无参的，语句体为空的构造方法。但如果已经手动定义了一个有参的构造器，就**不会** 再自动生成这个默认无参的构造器，此时再使用无参的构造器构造对象就是非法的。
* 构造方法总是通过`new`来调用的，如果使用的是没有参数的构造方法，则直接是`new <类名>()`来调用，如果有参数则需加上参数列表`new <类名>(参数列表)`，另外，构造方法与普通方法一样，是可以进行方法重载的。示例：
```java
public class Hero {
       
    String name; //姓名
       
    float hp; //血量
       
    float armor; //护甲
       
    int moveSpeed; //移动速度
       
    //带一个参数的构造方法
    public Hero(String heroname){ 
        name = heroname;
    }
     
    //带两个参数的构造方法
    public Hero(String heroname,float herohp){ 
        name = heroname;
        hp = herohp;
    }
       
    public static void main(String[] args) {
        Hero garen =  new Hero("盖伦"); //调用构造方法创建对象时需要加上参数了。
        Hero teemo =  new Hero("提莫",383);
    }
     
}
```

## this

* this可以顾名思义，this这个关键字代表当前对象，就相当于当前对象的名字，实际使用于类定义的内部。示例：
```java
public class Hero {
     
    String name; //姓名
     
    float hp; //血量
     
    float armor; //护甲
     
    int moveSpeed; //移动速度
 
    //打印内存中的虚拟地址
    public void showAddressInMemory(){
        System.out.println("打印this看到的虚拟地址："+this); //this在类内部使用，因为此时类没有名字，如果要用其中的属性很不方便，所以设置this来表示当前：“对象”，相当于类的一个虚拟名字。
    }
     
    public static void main(String[] args) {
        Hero garen =  new Hero();
        garen.name = "盖伦";
        //直接打印对象，会显示该对象在内存中的虚拟地址
        //格式：Hero@c17164 c17164即虚拟地址，每次执行，得到的地址不一定一样
 
        System.out.println("打印对象看到的虚拟地址："+garen);
        //调用showAddressInMemory，打印该对象的this，显示相同的虚拟地址->表示this起始和对象名garen指向的是同一个东西
        garen.showAddressInMemory();
    }
}
```
* 使用this给对象的属性赋值。示例：
```java
public class Hero {
     
    String name; //姓名
     
    //参数名和属性名一样
    //在方法体中，只能访问到参数name
    public void setName1(String name){
        name = name;
    }
     
    //为了避免setName1中的问题，参数名不得不使用其他变量名
    public void setName2(String heroName){
        name = heroName;
    }
     
    //通过this访问属性
    public void setName3(String name){
        //name代表的是参数name
        //this.name代表的是属性name
        this.name = name;
    }
     
    public static void main(String[] args) {
        Hero  h =new Hero();
         
        h.setName1("teemo");
        System.out.println(h.name); //结果为null，即参数的值传不到对象里的属性上
         
        h.setName2("garen");
        System.out.println(h.name); //结果为garen，成功，即使用this可以访问到当前对象的属性   
         
        h.setName3("死歌");
        System.out.println(h.name); //结果为死歌，成功，即使用非属性名的形参，还可以将值传给属性。    
    }
     
}
```
* this还可以用来在一个构造器内部调用另一个构造器。调用的形式为`this(要调用的构造器的参数)`。在一个构造器中调用另一个构造器的的语句只能放在该构造器的第一条语句。
  
## 隐式参数与显式参数

* 隐式参数是出现在方法之前的实例字段，在方法中被直接调用。而显式参数就是普通的位于方法名后面括号中的参数。
* 隐式参数常用this来指示，以便和局部变量区分开来。
* 示例：
```java

public class Employee {
    double salary;

    public void raiseSalary (double byPercent) {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```
* 在这个例子中，salary为隐式参数，而byPercent为显式参数。
* 可以用this指示隐式参数：
```java

public class Employee {
    double salary;

    public void raiseSalary (double byPercent) {
        double raise = this.salary * byPercent / 100;
        this.salary += raise;
    }
}
```

## 参数的传递

* 参数与变量一样，分为基本类型和类类型。基本类型参数与c语言基本一样，而类类型的参数有一点类似c语言中的指针参数。
* 类类型参数可以修改实际的类类型的变量指向的对象，实际类类型变量是对应对象的引用，是对象的一个地址。示例：
```java
public class Hero {
        
    String name; //姓名
        
    float hp; //血量
        
    float armor; //护甲
        
    int moveSpeed; //移动速度
     
    public Hero(){
         
    }
     
    public Hero(String name,float hp){
        this.name = name;
        this.hp = hp;
    }
 
    //复活
    public void revive(Hero h){ //传入的参数是Hero类型的引用
        h = new Hero("提莫",383);
    }
 
    public static void main(String[] args) {
        Hero teemo =  new Hero("提莫",383);
         
        //受到400伤害，挂了
        teemo.hp = teemo.hp - 400;
         
        teemo.revive(teemo); // teemo中hp的值变为了383，即通过类类型传递的是可以在函数内部修改的。
         
    
         
    }
      
}
```
* 在给参数命名时，可以在名字面前加上前缀a以与实例字段区别。如`name = aName`.

## 包

* 把具有某种关系的类放在一个包里。包必须在**类最开始的地方声明**。
* 借助包名可以确保类名的唯一性。包名常使用因特网域名的逆序形式。如域名为`horstman.com`则将包名设为`com.horstman`.包名之后还可以追加一个工程名之后再写上类名。如`com.horstman.corejava.Employee`，这个也被称为该类的**完全限定名**.其中corejava为工程名，Employee为类名。
* 示例：
```java
package charactor; //在最开始的地方声明该类所处于的包名
public class Hero {
        
    String name; //姓名
        
    float hp; //血量
        
    float armor; //护甲
        
    int moveSpeed; //移动速度
     
}
```
* 包与类的关系示例：
![java](https://gitee.com/zhangjie0524/picgo/raw/master/uPic/java.jpg)

### 类的导入

* 一个类可以使用所属包中的所有类，以及其他包里的公共类。但是其他包里的公共类必须使用`import`来导入。（也可以在使用其他包里的公共类时使用其完全限定名）
* 使用`import 包名.*`可以导入一个包里的所有类。（但是只能使用`*`导入一个包，不能导入一个包里嵌套的所有包。
* 示例：
```java
package charactor;
 
//Weapon类在其他包里，使用必须进行import
import property.Weapon;//格式为 import 类的完全限定名;
 
public class Hero {
        
    String name; //姓名
        
    float hp; //血量
        
    float armor; //护甲
        
    int moveSpeed; //移动速度
     
    //装备一把武器
    public void equip(Weapon w){
         
    }
        
}
```

### 静态导入

* 在import关键字之后加上static修饰符可以导入某个类中的静态方法和静态字段。如：`import static java.lang.System.*`可以导入System类中的所有静态方法和静态字段。如果这样导入，`System.out.print()`就可以用`out.print()`代替（可以省略类名）。当然，也可以导入特定的方法和字段。如`import static java.lang.System.out`.

### 在包中增加类

* 要将类放入包中需要将包的名字放在该类源文件的开头。如`package com.horstman.corejava`.如果在源文件开头没有防止package语句，则这个类就默认属于**无名包**（没有名字，但是实际存在的的包）。还要注意**类的源文件必须放到与完整包名匹配的目录中**。
* 编译和运行类必须切换到基目录。

### 类路径

* 类的路径必须与包名相匹配。
* 通过设置`classpath`来设置类路径，以使多个程序共享类。

### JAR文件

* **JAR文件**:java的压缩包文件（使用zip格式）。在一个JAR文件中可以包含多个压缩形式的类文件和子目录，也可以包含诸如图像、声音等类型的文件。在程序中使用第三方的库文件时，需要得到相应的JAR文件。
* **创建JAR文件**：使用`jar`工具来制作JAR文件。类似Unix系统中的`tar`指令。[jar程序选项](https://www.cnblogs.com/chenjfblog/p/10164967.html
* **清单文件**：每个JAR文件都包含一个清单文件（manifest），用于描述JAR文件的某些特性。[清单文件具体使用](https://blog.csdn.net/weixin_33801856/article/details/86247641).
* **可执行JAR文件**：需要为JAR包装的程序指定入口点，即在需要调用java程序启动器时指定的类。可以使用`jar`命令的e选项，来指定入口点。


## 成员变量的修饰符

### 类之间的关系

* **依赖**："use-a"关系，即一个类的方法使用或者操纵另一个类的对象，就是一个类依赖于另一个类。
* **聚合**："has-a"关系，即一个类中的对象包含另一个类的一些对象。
* **继承**："is-a"关系，表示一个更特殊的类与更一般的类之间的关系。，这个更特殊的类中不但包含了原来的类中的所有对象和方法，还增加一些额外的功能。
* **UML**:unified Modeling Language:统一建模语言，用来绘制类图。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200922073144.jpg)

### private

* 使用private修饰的变量，只有这种类的对象才可以访问，子类不可以继承，其它的类就更不能访问了。

### 没有修饰符

* 没有修饰符的成员变量，自身的对象可以访问，同包的类可以访问，同包子类可以继承，不同包子类也可以继承，但是不同包的类不可以访问。

### proteced

* 使用protected修饰的成员字段或者方法，同包类可以访问和继承，不同包的类不可以访问和继承。


### public

* 任何地方，都可以访问和继承。
* 在一个源文件中（.java）中只能由**一个public类**，但可以有任意数目的非公共类。
* 由一个源文件编译而成的类文件（.class），将包含main方法的类名提供给解释器以启动这个程序。

## 类属性（static）

* 当类中的属性被static修饰时，这个属性就叫做**类属性**，又叫做**静态属性**或**静态字段**。如果某个属性被声明为类属性，那么该类所有的对象都共享这个值,不管有没有实例化得到的对象，这个属性都存在，不管有多少个对象，都共用一个静态字段，静态字段只属于类，不属于任何单个的对象。静态属性中常用的是**静态常量**。
* 与类属性相对的（类中没有static修饰的属性）叫做**对象属性**，又叫做**非静态属性**，**实例属性**。示例：
```java
package charactor;
 
public class Hero {
    public String name; //实例属性，对象属性，非静态属性
    protected float hp;
    static String copyright;//类属性,静态属性
     
    public static void main(String[] args) {
           Hero garen =  new Hero();
           garen.name = "盖伦";
            
           Hero.copyright = "版权由Riot Games公司所有"; //对类属性的赋值
            
           System.out.println(garen.name);
           System.out.println(garen.copyright);
            
           Hero teemo =  new Hero();
           teemo.name = "提莫";
           System.out.println(teemo.name);    
           System.out.println(teemo.copyright);
         
    }
     
}
```
* 对类属性的赋值通过直接使用类名来完成`Hero.copyright = `.也可以通过实际的对象来调用，不过一般还是使用类来直接调用，这样更符合类对象的概念。

## 类方法（静态方法）

* **类方法**，又叫静态方法。同类对象相似，类方法也是通过在方法名前面加上`static`关键字来实现的。
* 静态方法不使用对象中的实例字段（也可以理解为静态方法中没有this参数，它所需要的所有参数都通过显示参数提供），计算结果与实际对象无关。
* 与类方法相对的是**对象方法**，对象方法又叫实例方法，非静态方法。示例：
```java
package charactor;
 
public class Hero {
    public String name;
    protected float hp;
 
    //实例方法,对象方法，非静态方法
    //必须有对象才能够调用
    public void die(){
        hp = 0;
    }
     
    //类方法，静态方法
    //通过类就可以直接调用
    public static void battleWin(){
        System.out.println("battle win");
    }
     
    public static void main(String[] args) {
           Hero garen =  new Hero();
           garen.name = "盖伦";
           //必须有一个对象才能调用
           garen.die();
            
           Hero teemo =  new Hero();
           teemo.name = "提莫";
            
           //无需对象，直接通过类调用
           Hero.battleWin();
         
    }
}
```
* **对象方法必须用实际创建的对象才能调用**，而类方法可以使用类来直接调用，也可以使用对象来调用。（同类对象的情况一致）。
* 当某个方法没有涉及到具体对象的属性时，设计为类方法，而当涉及具体对象的属性时，则一般设计为对象方法。示例：
```java
    public String getName(){
    	return name;
    }

    public static void printGameDuration(){
        System.out.println("已经玩了10分50秒");
    }
```

### 工厂方法

* 静态方法的另一个用途就是静态工厂方法，工厂方法实际上是构造器方法的延伸。使用工厂方法可以生成不同风格的对象。

### main方法

* main方法启动时还没有任何对象，所以main方法不对任何对象进行操作，main方法必须声明为static方法。
* 每个类都可以有一个main方法，用于对每个类进行单元测试。
## 属性初始化

* 对象属性初始化。
  1. 在声明时初始化；
  2. 在块中初始化，初始化块的前面还是可以加上修饰符的；
  3. 在构造方法中初始化。
  4. **初始化的顺序**：如果三种初始化方式同时出现，则不管构造方法中初始化的相对位置在哪里，它的初始化都是最后执行的。
  5. 示例：
```java
public class Hero {
    public String name = "some hero"; //声明该属性的时候初始化
    protected float hp;
    float maxHP;
     
    {
        maxHP = 200; //初始化块,单独用花括号给出一个用来初始化属性的块。
    }  
     
    public Hero(){
        hp = 100; //构造方法中初始化
         
    }
     
}
```

* 类属性初始化
  1. 声明时初始化
  2. 静态初始化块:在普通花括号形成的块前面加上关键字`static`形成静态初始化块。
  3. 示例：
```java
public class Hero {
    public String name;
    protected float hp;
    float maxHP;
     
    //物品栏的容量
    public static int itemCapacity = 8; //声明的时候 初始化
     
    static{
        itemCapacity = 6;//静态初始化块 初始化
    }
     
    public Hero(){
         
    }
     
    public static void main(String[] args) {
        System.out.println(Hero.itemCapacity);
    }
     
}
```

## 单例模式

* **单例模式**又叫**Singleton**模式，表示的是一个类，在一个JVM（Java虚拟机）中只有一个实例存在。

### 饿汉式单例模式

* 饿汉式单例模式通过使用private使构造方法无法在外部通过new来创建对象，并创建一个新的方法指定在类中定义的对象，每次使用该方法都只能产生一个唯一的对象从而实现单例模式。
```java
public class GiantDragon {
 
    //私有化构造方法使得该类无法在外部通过new 进行实例化
    private GiantDragon(){
         
    }
 
    //准备一个类属性，指向一个实例化对象。 因为是类属性，所以只有一个
 
    private static GiantDragon instance = new GiantDragon();
     
    //public static 方法，提供给调用者获取前面定义的instance对象
    public static GiantDragon getInstance(){
        return instance;
    }
     
}
```
### 懒汉式单例模式

* 懒汉式与饿汉式的区别在于懒汉式只有在调用创建对象的方法时才第一次创建对象。
```java
public class GiantDragon {
  
    //私有化构造方法使得该类无法在外部通过new 进行实例化
    private GiantDragon(){       
    }
  
    //准备一个类属性，用于指向一个实例化对象，但是暂时指向null
    private static GiantDragon instance;
      
    //public static 方法，返回实例对象
    public static GiantDragon getInstance(){
        //第一次访问的时候，发现instance没有指向任何对象，这时实例化一个对象
        if(null==instance){
            instance = new GiantDragon();
        }
        //返回 instance指向的对象
        return instance;
    }
      
}
```

## 枚举类型

* 枚举类型包括有限个命名的值。例如：
```java

enum Size{SMALL, MEDIUM, LARGE, EXTRA_LARGE};//定义枚举类型Size。
Size s = Size.MEDIUM;//声明枚举类型的变量s并进行初始化。
```
* 枚举类型的变量中只能存储这个类型的声明中给定的**某个枚举值**，或者null（表示这个变量没有设置任何值）。

# 接口与继承

## 接口（Interface）

* 接口不是类，而是对希望符合这个接口的类的一组需求（应该做什么）。接口是抽象的，它的所有成员函数都是抽象函数（语句体都是空的），它的所有成员变量都是`public static final`类型（但是在接口中声明的方法都默认是public方法，所以public可以省略）。
* 接口的创建：
```java
package charactor;
 
public interface AD { //接口的创建使用关键字interface。
        //物理伤害
    public void physicAttack(); //接口的成员函数都是抽象函数，只有其形，而实际里面什么也没有。
}
```
* 接口的使用：（接口在类中具体实现时的public不能省略）
```java
package charactor;
 
public class ADHero extends Hero implements AD{ //ADHero是从Hero继承而来的的子类，并且使用关键字implements加入了AD接口

    @Override
    public void physicAttack() { //接口在实际使用的时候再定义具体操作的实现。
        System.out.println("进行物理攻击");
    }
 
}
```
    * 接口使用关键字`implements`来加入，并且可以同时加入多个接口，如`...implements AD,AP`.

* 
## 对象转型

### 引用类型和对象类型

* 在`Hero a = new Hero()`中，a是引用，a的类型即是引用类型（此例中为a前面的Hero类类型），而`new Hero()`创建的就是对象，对象类型就是Hero类类型。

### 子类转父类（向上转型）

* 类型转换发生在引用类型和对象类型不一致的时候。（类似基本类型中`=`两边的类型不一致时。）类型转换不一定会成功。（就像基本类型转换也会有失败的时候，就像int不能转换为double）。子类是可以转换为父类的（就像基本类型中，长的可以转换为短的，如double可以转换为int）。

### 父类转子类（向下转型）

* 父类转子类需要进行强制类型转换，如`a  = (ADHero)h`.

### 没有继承关系的类

* 没有继承关系的类之间转换一定会失败，即使用强制类型转换也会出现异常报错。

### 实现类转换为接口(向上转型)

### 接口转换为实现类（向下转型）

## instanceof语句

* instanceof语句用来判断一个引用所指向的对象是否是某种类的实例化或者其子类的实例化。使用示例：`h instanceof Hero`判断引用h指向的对象是否是Hero类或者Hero子类的，如果是则结果为true，否则为false。

## 重写

* 子类可以继承父类的对象方法，如果子类对从父类继承过来的对象方法进行了修改（即在子类中对相同名字的对象方法在写一遍，故称为重写），这就叫做方法的重写。示例：
```java
package property;
 
//父类
public class Item {
    String name;
    
    public void effect() {
        System.out.println("物品使用后，可以有效果");
    }
 
}

//从Item中继承的子类
public class LifePotion extends Item{
     
     //对Item中的effect方法进行了重写
    public void effect(){
        System.out.println("血瓶使用后，可以回血");
    }
     
}
```

## 多态

### 操作符的多态

* 操作符的多态是指同一个操作符在不同的情景下的作用不同。如`+`，在算术运算中是加法的作用，而在字符串中是连接字符串的作用。

### 类的多态

* 同一个类的同一个方法，输出不同的结果是类的一种多态现象。示例：
```java
package property;
 
public class Item {
    String name;
    int price;
 
    public void buy(){
        System.out.println("购买");
    }
    public void effect() {
        System.out.println("物品使用后，可以有效果 ");
    }
     
    public static void main(String[] args) {
        Item i1= new LifePotion(); //LifePotion和MagicPotion是类Item的两个子类。而且这两个子类中都有方法的重写。
        Item i2 = new MagicPotion(); //引用是父类类型的。
        System.out.print("i1  是Item类型，执行effect打印:"); //由于两个子类的重写方法不同，导致调用同一个方法会有不同的输出
        i1.effect();
        System.out.print("i2也是Item类型，执行effect打印:");
        i2.effect();
    }
 
}
```

* 实现类的多态的条件:
  1. 父类（接口）指向子类的对象；
  2. 调用的方法被重写。

### 对象变量的多态

* 一个对象变量可以指示多种实际类型的现象称为多态。
* 这种情况常出现在父类和子类的对象中。如,父类为Father，子类为Kid。
```java

var people = new Father[2];

Kid person1 = new Kid();
Father person2 = new Father();

for(Father e : people) {
    e.age++;
}
```
  * 在这个例子中，对象变量e既有可能指向Father类型，也有可能指向Kid类型。
## 隐藏

* 与重写类似。重写是子类对父类的**对象方法**的覆盖，而隐藏是对父类的**类方法的覆盖**。示例：
```java
package charactor;
  
public class Hero {
    public String name;
    protected float hp;
  
    //类方法，静态方法
    //通过类就可以直接调用
    public static void battleWin(){
        System.out.println("hero battle win");
    }
      
}

public class ADHero extends Hero {
  
    //隐藏父类的battleWin方法
    public static void battleWin(){
        System.out.println("ad hero battle win");
    }   
     
    public static void main(String[] args) {
        Hero.battleWin(); //输出的是hero battle win
        ADHero.battleWin(); //输出的是ad hero battle win
    }
  
}
```

## super关键字

* super是在子类中调用父类中的属性，方法的关键字。
    1. 显式调用带参的父类构造方法；如`super(参数)`
    2. 调用父类的属性：如`super.name`
    3. 调用父类的普通方法:如`super.useItem()`.

## Object类

* Object默认是所有类的父类。（全名：java.lang.Object:java.lang这个包是默认导入到每一个类中的）
* Object类中提供的方法所有类都默认含有。
* Objiect类中有很多方法，如`toString(), finalize(),equals()...`。

### Object类型的变量

* 可以使用Object类型的变量引用所有类型的对象。如：`Object obj = new Employee();`。（注意：除了基本类型（int，char，boolean...)不是对象，其他所有类型都是对象。） 
* 所有的数组类型，不管是基本类型的数组还是对象数组都是Object类的扩展。如
```java
Employee[] staff = new Employee[10];
obj = staff; //ok
obj = int[10]; //ok
```

### equals方法

* Object中equals的实现：
```java
    //第一种
 public boolean equals(Object obj) {
   return (this == obj);
   //第二种
```
* Objects类中equals的实现：
```java

   static boolean equals(Object a, Object b) {
       ...
   }
```

* equals方法是用来检测一个对象是否等于另一个对象的(Object中的equals方法适用于两个参数都不为null的情况，Objects类中的equals方法两个参数都为null时返回true，一个为null是返回false，两个都不为null时**返回a.equals(b)的结果**，即进行正常比较。不过object类中直接判断两个对象的引用是否相等来判断对象是否想等的方法有时会不够，所以equals方法经常会在子类中被**重写**。如：
```java
public class Employee{
    ...
    @override //用@override标记来表明这是对超类方法的覆盖，以避免出现参数类型不一致等情况（会报错）
    public boolean equals(Object otherObject){//参数类型必须为Object才能覆盖Object类中的equals方法
        //快速检查对象是否相同
        if(this==otherObject) return true;
        
        //如果EcPLID参数为空，则必须返回false
        if(otherObject==null) return false;
        
        //如果类不匹配，它们就不能相等。
        if(getClass()!=otherObject.getClass())
            return false;
        
        //现在我们知道另一个对象是非空雇员，将其强制类型转换为对应的类型
        Employee other =(Employee)otherObject;
        
        //测试字段是否具有相同的值
        return Object.equals(other.name);
        && salary==other.salary
        && hireDay.equals(other.hireDay);
    }
}
```
* equals方法的设计一般要遵循**自反性**，**对称性**，**传递性**，**一致性**，**非空性**。

### hashCode方法

* 散列码是由对象导出的一个整型值。没有规律，两个不同的对象的散列码基本不会相同。Object类的散列码是由对象的存储地址导出的。
* hashCode方法：`int hashCode()`。返回对象的散列码。

### toString方法

* toString方法会返回表示对象值的一个字符串：类名[字段值]。
* Object类中的toString方法会打印对象的类名和散列码。toString 方法经常会在子类中被重写。如：
```java
public String toString() {
    return getClass().getName() + "name=" + name +"salary=" + salary;
}
```
* 使用getClass和getName方法确保子类也可以调用该方法。
* 只要一个对象与一个字符串通过`+`相连，java编译器就会自动地调用toString方法来或得这个对象的字符串描述并与另一个字符串相连。


## final修饰词

* final在修饰类、方法、基本类型变量、引用是分别有不同的意思。

### final修饰类

* final修饰类时表示该类不能被继承。使用示例：
```java
package charactor;
 
public final class Hero extends Object {
        
    String name; //姓名
        
    float hp; //血量
        
}
```

### final修饰方法

* 如果类中的方法被final修饰，则代表该方法不能在子类中被重写。使用示例：
```java
public class Hero {
        
    String name; //姓名
        
   
     
    public final void useItem(){
        System.out.println("hero use item");
    }   
     
  
    public static void main(String[] args) {
        new Hero();
    }
      
}
```

### final修饰基本类型变量

* final修饰基本类型变量表示该类型只有一次赋值机会（即变量在第一次被手动初始化后便是只读的变量，再不可修改了），如：`final int hp = 2;`

### final修饰引用

* 被final修饰的引用代表该引用只有一次被赋予指向对象的机会（类似基本类型变量只有一次赋值机会）。

## 抽象类

### 抽象方法

* 没有实现体的方法，是抽象方法。抽象方法使用`abstract`关键字标识。示例：`public abstract void attack();`

### 抽象类

* 包含抽象方法的类必须声明为抽象类，使用关键字`abstract`。
* 没有包含抽象方法的类也可以声明为抽象类。
* 抽象类不可以被直接实例化。即不可以使用`new`来创建抽象类的对象。但是**抽象类类型的引用变量**却是可以声明的。如果Person是一个抽象类，`new Person()`是错误的，但是`Person p;`却是可行的。
* **抽象类与接口区别**：一个子类只可以继承一个抽象类，但是可以实现多个接口。抽象类和接口都是为子类的具体实现提供了一个框架。
* 抽象类与接口中都可以包含实体的方法，这些实体方法被叫做**默认方法**。
* 示例：
```java
public abstract class Hero { //声明为抽象类
    String name;
             
    public static void main(String[] args) {
        //虽然没有抽象方法，但是一旦被声明为了抽象类，就不能够直接被实例化
        Hero h= new Hero();
    }
          
}
```

## 内部类

* 在一个类内部声明的类就是**内部类**，相应的外面的类为**外部类**

### 非静态内部类

* 直接在类内部定义(类前面没有任何修饰词），只有在外部类存在的时候才有意义。实例化的语法：`new <外部类>().new <内部类>`或者`<外部类引用>.new <内部类>`.示例：
```java
package charactor;
 
public class Hero {
    private String name; // 姓名
 
    // 非静态内部类，只有一个外部类对象存在的时候，才有意义
    // 战斗成绩只有在一个英雄对象存在的时候才有意义
    class BattleScore { //直接在内部定义，前面没有修饰词
        int kill;
        int die;
        int assit;
 
        public void legendary() {
            if (kill >= 8)
                System.out.println(name + "超神！");
            else
                System.out.println(name + "尚未超神！");
        }
    }
 
    public static void main(String[] args) {
        Hero garen = new Hero();
        garen.name = "盖伦";
        // 实例化内部类
        // BattleScore对象只有在一个英雄对象存在的时候才有意义
        // 所以其实例化必须建立在一个外部类对象的基础之上
        BattleScore score = garen.new BattleScore();
        score.kill = 9;
        score.legendary();
    }
 
}
```

### 静态内部类

* 静态内部类在外部类里面定义时加上了`static`修饰，此时的内部类与普通类相比，除了内部类可以访问外部类的私有静态成员外，没有任何区别。
* 静态内部类不依赖于外部类的对象，所以可以直接实例化。如`h = new Hero.EnemyCrystal()`.
* 示例：
```java
package charactor;
  
public class Hero {
    public String name;
    protected float hp;
  
    private static void battleWin(){
        System.out.println("battle win");
    }
     
    //敌方的水晶
    static class EnemyCrystal{
        int hp=5000;
         
        //如果水晶的血量为0，则宣布胜利
        public void checkIfVictory(){
            if(hp==0){
                Hero.battleWin();
                 
                //静态内部类不能直接访问外部类的对象属性
                System.out.println(name + " win this game");
            }
        }
    }
     
    public static void main(String[] args) {
        //实例化静态内部类
        Hero.EnemyCrystal crystal = new Hero.EnemyCrystal();
        crystal.checkIfVictory();
    }
  
}
```
### 匿名类

* 对于抽象方法，本来应该在子类中对其实现后，再实例化。但是**匿名类**是在实际使用这个抽象方法的时候直接对其现场实现，省去了在子类中实现的步骤，因而没有子类的名字，叫做匿名。但是，实际上系统是自动为这个你未曾创建的子类分配了一个名字。
* 示例：
```java
package charactor;
   
public abstract class Hero {
    String name; //姓名
             
    public abstract void attack(); //抽象方法
      
    public static void main(String[] args) {
          
        ADHero adh=new ADHero();
        //通过打印adh，可以看到adh这个对象属于ADHero类
        adh.attack();
        System.out.println(adh);
          
        Hero h = new Hero(){ //对抽象类在实例化时直接实现抽象类，省去了在子类中实现的步骤，从而没有类名，故为匿名类。
            //当场实现attack方法
            public void attack() {
                System.out.println("新的进攻手段");
            }
        };
        h.attack();
        //通过打印h，可以看到h这个对象属于Hero$1这么一个系统自动分配的类名
          
        System.out.println(h);
    }
      
}
```

### 本地类

* 本地类可以看做有名字的匿名类，都是在实际使用的代码块里对抽象方法进行实现，只是本地类还顺手创建了子类的名字。示例：
```java
package charactor;
   
public abstract class Hero {
    String name; //姓名
      
    public abstract void attack();
      
    public static void main(String[] args) {
          
        //与匿名类的区别在于，本地类有了自定义的类名
        class SomeHero extends Hero{ //s使用时创建了Hero的子类SomeHero
            public void attack() {
                System.out.println( name+ " 新的进攻手段");
            }
        }
         
        SomeHero h  =new SomeHero();
        h.name ="地卜师";
        h.attack();
    }
      
}
```

## 默认方法

* 在接口中除了抽象方法，还可以实现具体的方法，这个实现了的方法就是默认方法。默认方法前使用`default`来修饰。示例：
```java 
package charactor;
 
public interface Mortal {
    public void die(); //抽象方法
 
    default public void revive() { //默认方法
        System.out.println("本英雄复活了");
    }
}
```

# 注释

1. `//`方式：其注释内容从//开始到本行末尾。
2. `/* */`方式：其注释内容从`/*`开始到`*/`结束。
3. 文档注释：从`/**`开始到`*/`结束。

## 文档注释

* 文档注释借助于javadoc工具实现，它可以由源文件生成一个HTML文档。
* 在注释中包含**标记**和自由格式的文本(在其中可以使用HTML修饰符)。每个标记以`@`开始，如`@return`.

### 类注释

* 类注释放在`import`语句之后，类定义之前。

### 方法注释

* 方法注释放在所描述的方法之前。通常会使用标记。
* `@param`：用以描述当前方法的参数(parameters),可以占据多行。
* `@return`:用以描述当前方法的返回信息，同样可以占据多行。
* `@throws`：表示这个方法有可能抛出异常。

### 字段注释

* 对公共字段（通常为静态常量）建立文档。

### 通用注释

* `@since`：建立一个描述这个特性的版本的文本。
* `@author`:描述作者，可以有多个这个标记，每个标记对应一个作者。
* `@version`:描述当前版本。
* `@see`和`@link`：可以在之后放指向其它类或方法，以及URL的超链接。

### 包注释

* 在每个包的目录下创建一个名为package-info.java（包含一个Javadoc文档，在文档后面是一个package语句）或者package.html的文件（使用普通的html即可，javadoc会抽取`<body>...</bode>`的部分）.

### 文档注释的抽取

* 使用[javadoc](https://www.cnblogs.com/fjhh/p/5370642.html).

# 异常、断言和日志

## 异常

### 异常概念

* **异常处理的任务**：将控制权从产生错误的地方转移到能够处理这种情况的错误处理器。
* **程序中可能会出现的错误**：
  * 用户输入错误；
  * 设备错误；
  * 物理限制（存储空间）；
  * 代码错误。
* **异常处理过程**： 如果某个方法不能够正常的完成，可以通过抛出一个封装了错误信息的异常对象来退出方法。需要退出的方法并不返回任何值，而是直接退出，之后异常处理机制开始搜索能够处理这种异常的异常处理器。

### 异常分类

* **异常对象**：是派生于Throwable类的类实例。
* **异常的层次结构**：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201015184846.jpg)
    * 所有的异常类都是由Throwable类继承而来。
    * **Error**类层次结构：描述了java运行时的系统内部错误和资源耗尽错误。
    * **Exception**类层次结构：是设计程序时主要关注的异常。
    * **RuntimeException**:由编程错误导致的异常（如果出现RuntimeException异常，一定是程序员的问题）。具体包含：
      * 错误的强制类型转换；
      * 数组访问越界；
      * 访问null指针。
    * **IOException**:包含除RuntimeException的其他异常，例如：
      * 试图超越文件末尾继续读取数据；
      * 试图打开一个不存在的文件；
      * 试图根据给定的字符串查找并不存在的Class对象。
* **非检查型异常与检查型异常**：所有派生于Error或者RuntimeException类的异常称为非检查型异常。其余异常为检查型异常。

### 声明检查型异常

* 在方法首法使用`throws`关键字声明该方法可能抛出的**检查型异常**：如： `public FileInputStream(String name) throws FileNotFoundException`。如果会抛出多个异常，可以在首部声明所有的检查型异常类,用逗号分隔，如：`public Image loadImage(String s) throws FileNotFoundException, EoFException`
* 一个方法必须声明所有可能抛出的检查型异常。而非检查型异常是我们无法控制的（Error），或者是我们应该极力在编程时避免的（RuntimeException）。
* 子类方法中声明的检查型异常是父类方法中的声明的异常的子集。

### 抛出异常

* 抛出异常的方法：
  1. 找到一个合适的异常类；
  2. 创建这个类的对象：如：`var e = new EOFException`
  3. 将对象抛出：如`throw e`。
* 2、3步可以合并为一步：`throw new EOFException`
* 每个异常类都带有一个字符串参数的构造器，可以用来描述异常的具体信息。如：
```java
String gripe = "Content-length: " + len +", Recived: " + n;
throw new EOFException(gripe);
```
### 创建异常类

* 如果标准的异常类不能描述清楚你程序的问题，那么就需要创建自己的异常类。
* 自定义的异常类需要派生于Exception类或者Exception的子类。并且这个类中应该包含两个构造器：一个默认的构造器（无参数），一个包含描述异常信息的字符串参数的构造器。示例：
```java
class FileFormatException extends IOException {
    public FileFormatException() {} //默认的构造器
    public FileFormatException (String gripe) {
        super(gripe);//父类构造器中有含这个参数的构造器，直接借用即可
    }
}
```

### 捕获异常

* 抛出异常是将发生的异常交给异常处理器取处理。而与之相对的**捕获异常**就是将异常交给用户指定的异常处理器去处理。
* 捕获异常需要使用`try/catch`语句块，要捕获异常的方法就不再使用`throws`声明抛出异常。示例：
```java
    public void read(String filename) {
        try {
            var in = new FileInputStream(filename);
            int b;
            while (b = in.read() != -1) {
                process input
            }
        }
        catch (IOException exception) {
            exception.printStackTrace(); //调用对应异常的处理器方法
        }
    }
```
* **捕获多个异常**：在一个try语句块中可以捕获多个异常类型，并对不同的异常类型做出不同的处理。例如：
    ```java
    try {
        //code that might throw exceptions
    }
    catch (FileNotFoundException e) {
        //emergency action for missing files
    } 
    catch (IOException e) {
        //emergency action for all other I/O problems
    }
    ```java
        * 还可以用一个catch语句捕获多个异常类型，前提是这些异常类型彼此之间不存在子类关系。如：
    ```java

    try {
        //code that might throw exceptions
    }
    catch (FileNotFoundException e | UnknownHostException e) { //同时捕获多个异常
        //emergency action for missing files or unknown hosts
    } 
    catch (IOException e) {
        //emergency action for I/O problems
    }
    ```
* **再次抛出异常**：可以在catch语句中仅记录一个异常（即*不对该异常对象做修改*），之后再将这个异常重新抛出。此时可以在方法上重新加上`throws`关键字，指明抛出的异常类型。示例：
```java
try {
    //access thr database
}
catch (Exception) {
    logger.log(level, message, e);//仅仅是记录该异常的信息
    throw e;
}
```

### finally子句

* 代码抛出一个异常时，会停止处理这个方法中的剩余的代码，并退出这个方法。但此时可能会有这个方法以及获得的资源没有清理。而finally子句正是用来清理这这些资源的。
* 如果无论该方法有没有抛出异常，finally子句中的代码都会在前面代码按照普通流程结束后执行（没有异常则顺序执行到finally子句，捕获了异常则再catch中处理了异常再执行finall子句，抛出了异常则抛出异常后执行finally子句），示例：
```java
var in = new FileInputStream;
try {
    //code
}
catch (IOException) {
    //...
}
finally {
    in.close();
}
```
* 还可以将两个try嵌套，内层try确保关闭资源，外层try语句确保报告错误。示例：
```java
InputStream in = ...;
try {
    try {
        //code that might throw exception
    }
    finally {
        in.close();
    }
}
catch (IOException) {
    //...
}
```

### try-with-Resources语句

* try-with-Resources语句是和finally子句实现同样功能的。可以在try后面加上执行完代码后需要关闭的资源，这样构成try-with-Resources语句,无论什么时候退出try语块，都会自动将资源关闭。示例：
```java
try (var in = new Scanner(new FileInputStream("/usr/share/dict/words"), StandardCharests.UTF_8)) {
    while (in.hasNext()) {
        System.out.println(in.next());
    }
}
```
* try-with-Resources语句也可以带上catch子句和finally子句。

### 分析堆栈轨迹元素

# 并发

## 线程与进程

* 每个进程(processor)都拥有自己的一套变量，而线程(thread)之间共享数据。线程比进程更加的轻量级。
* 线程是在进程内部同时做的事情。
* 多线程即在同一时间，可以做多件事情。

## 创建多线程

### 继承线程类创建多线程

* 可以通过继承`Thread`类来实现创建线程，如：
```java
public class KillThread extends Thread{ //KillThread是继承自Thread的子类
     
    private Hero h1;
    private Hero h2;
 
    public KillThread(Hero h1, Hero h2){
        this.h1 = h1;
        this.h2 = h2;
    }
 
    public void run(){ //覆盖Thread中的run方法（必须），以实现启动线程后的具体操作。
        while(!h2.isDead()){
            h1.attackHero(h2);
        }
    }
}
```
* 无论使用什么方法实现线程，线程启动都需要使用Thread类中的**start方法**。线程启动示例：
```java
    KillThread killThread1 = new KillThread(gareen,teemo); //新建一个线程
    killThread1.start(); //启动一个创建的线程
    KillThread killThread2 = new KillThread(bh,leesin);
    killThread2.start();
```

### 实现Runable接口来创建多线程

* Runable接口中有一个run方法，实现这个接口的时候必须实现run方法（run方法中是这个线程需要做的事）。
* 实现Runable接口示例：
```java

public class Battle implements Runnable{ //实现Runable接口的类
     
    private Hero h1;
    private Hero h2;
 
    public Battle(Hero h1, Hero h2){
        this.h1 = h1;
        this.h2 = h2;
    }
 
    public void run(){ //实现run方法
        while(!h2.isDead()){
            h1.attackHero(h2);
        }
    }
}
```
* 线程启动示例：
```java
    Battle battle1 = new Battle(gareen,teemo); //启动的时候，首先创建一个Battle对象，然后再根据该battle对象创建一个线程对象，并启动 
    new Thread(battle1).start(); //把Battle对象作为Thread对象的构造器的参数来新建一个Thread对象，并直接调用start方法启动这个线程。
 
    Battle battle2 = new Battle(bh,leesin);
    new Thread(battle2).start();
```

### 使用匿名类创建多线程
。。。




# Java的API
---
实在是太多了，可以在需要时查看API的[官方文档](https://docs.oracle.com/en/java/javase/15/docs/api/index.html)

## java.lang.Object

* `Class getClass()`:返回包含对象信息的类对象。
* `boolean equals(Object otherObject)`:比较两个对象是否相等。
* `String toString()`:返回表示该对象值的字符串。

## java.lang.Class

* `String getName()`:返回这个类的名字；
* `Class getSuperclass()`:以Class对象的的形式返回这个类的超类。

## java.util.Objects

* 可以看做是Object类针对多个对象进行处理的类似的类。
* 判断两对象是否相等的方法：`static boolean equals(Object a, Object b)`。
* 提供散列码的方法（hashcode）:
  * `static int hash(Object...objects)`，返回一个散列码，由提供的所有对象的散列码组合得到。
  * `static int hashCOde(Object a)`如果a为null返回0，否则返回a.hashCode()的结果（即Object类中的hashCode方法增加了对null的处理）

## java.util.List

## Math

## java.time.LocalDate

## java.util.Random

* `Random()`返回一个随机数生成器（对应的类的对象）
* `int nextInt(int n)`，返回一个0~n-1之间的随机数的方法。

## java.util.ArrayList<E> （泛型数组列表）

* ArrayList类类似于数组，但是它能在添加或者删除元素时，**自动调整数组的容量**。
* ArrayList是有**类型参数**的**泛型类**（所以又被称为**泛型数组列表**），泛型类是可以在使用时再声明具体类型的。使用时为了指明数组保存的元素的类型，可以使用一对尖括号`<>`来将具体的类名追加到ArrayList后面。如`Array<Employee> staff = new ArrayList<Employee>();`.在这种方式中可以去掉后一个尖括号中的类型`Array<Employee> staff = new ArrayList<>(可以在这里填数组列表的容量,也可以不写。即使写了容量，这个容量仍是可以在使用时动态改变的);`,这种使用空的尖括号的方式又被称为**菱形语法**。
* 使用`boolean add(E obj)`方法可以将元素**加到数组列表**中，如`staff.add(i)`.`void add(int index, E obj)`。可以在数组内部指定位置插入元素，并使后面的元素后移，同时数组长度加一。
* `int size()`方法返回数组列表中现在的元素个数。如`length = staff.size()`.
* 不能使用普通的`[下标]`来访问数组列表中的元素。使用`get()`方法来访问数组列表中第i个元素，如`value = staff.get(i)`。使用`set()`方法来对第i个元素进行赋值。如`staff.set(i, value)`.
* `remove()`方法删除指定位置的元素，并将之后的所有元素前移，返回所删除的元素。如`staff.remove(i)`.
* `void ensureCapacity(int capacity)`方法可以给数组分配一个有具体数量的数组空间如：`staff.ensure(100)`。与直接在创建数组列表时声明大小的效果一样。
* 遍历：泛型数组列表同样可以用`for each`循环来遍历每个元素。


## java.util.Stack<E>

* 这是java用于实现栈功能的类。
* 初始化一个空栈：`Stack<Interger> stack1 = new Stack<Interger>();`,因为栈也是使用泛型的，所以初始化的时候需要**指定类型**。
* 判断栈是否为空:`stack1.empty()`,方法`boolean empty()`
* 查看栈顶部的元素但不取出：`stack1.peek()`,方法`Object peek()`，Object是指返回值的类型是由初始化的时候指定的，具体为哪种并不确定。
* 进栈：`stack1.push(Object element);`，方法`Object push(Object element)`
* 出栈：`stack1.pop();`,方法`Object pop()`.
* 返回某个值在堆栈中的位置从，位置是从1开始的：方法`int search(Object element)`.

## java.util.Arrays

* 这是一个主要用来对数组进行处理的类。
* 判断两个数组是否相等的静态方法：`static boolean equals(xxx[] a, xxx[] b)`.如果两个数组长度相同且对应位置的元素相等，则返回true，否则返回false。
* 打印数组:`Arrays.toString(数组名)`。结果是一个形如"[1, 2, 3, 4]"的字符串。打印多维数组需要调用`Arrays.deepToString(数组名)`。
* 拷贝数组`数组名1.toArray(数组名2)`。将数组1的数组元素拷贝到数组2中去。

## java.lang.Integer

* `int intValue()`:将该Integer的对象的值作为一个int返回。
* `static String toString(int i)`:返回一个String对象，表示指定数值的十进制表示。
* `static String toString(int i, int radix)`：返回数值i基于radix参数指定进制的表示。
* `static int parseInt(String s)`：将字符串转换为十进制整型返回。
* `static int pardeInt(String s, int radix)：将字符串转换为radix进制整型返回。
* `static Integer valueOf(String s)`:返回一个Integer对象，用s表示的十进制整数初始化。
* `static Integer valueOf(String s, int radix)`：返回一个Integer对象，用s表示的radix进制数初始化。

## java.lang.Enum<E>

* `static Enum valueOf(Class enumClass, String name)`：返回给定类中指定名字的枚举常量。
* `String toString()`:返回枚举常量名。如`Size.SMALL.toString()`返回字符串"SMALL".
* `int ordinal()`：返回枚举常量在enum中声明的位置，位置从0开始计数。
* `int compareTO(E other)`:如果枚举常量出现在other之前，返回一个负整数；如果this==other，返回0； 其他情况返回一个正整数。

## java.lang.Comparable<T>

* 这是一个接口。其中要求了`int comparable(T other)`方法。这个方法要求对象小于other返回一个负整数，相等返回0，大于返回正整数。

## java.lang.Throwable(异常)

* `Thorwable()`:构造一个Throwable对象但是没有详细的描述信息
* `Throwable(String message)`: 构造一个Throwable对象，带有指定的详细描述信息。
* `String getMessage()`:获得Throwable对象的详细描述信息。















