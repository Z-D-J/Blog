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
* 所有被声明的变量都是有默认值的。例如：数字类型的默认值为0,引用类型的默认值为null。还有NULL，''等默认值。不过局部变量声明后不会进行默认的初始化。

# 常量

* 类似变量的定义声明，常量只需要在定义时在类型前加上关键词`final`。常量只能在定义时赋值初始化，之后不能再赋值。
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
* **字符串变量的创建**：`String s = new String(字符串字面量)`.用字符串字面量初始化字符串变量。也可以直接初始化一个字面量，如`String s = "hello"`。
* **字符串的连接**：使用`+`可以将两个字符串连接起来，如果`+`两边的不是字符串类型，它会自动将非字符串类型的转为字符串类型。
* **字符串的读入**：使用`in.next()`可以读入单词，每个单词之间用空格隔开。
* 字符串是只读的变量，不可以通过赋值来修改。

### 字符串的操作

* 字符串的数据是对象，可以通过`.`这个操作来实现对字符串的操作。
* **字符串的比较**：`s.compareTo(s1)`;
* **获得字符串的长度**：`s.length()`;
* **访问字符串中的单个字符**：`s.charAt(3)`.(3是字符的索引，类似数组)。
* **判断两个字符串是否相同**：`s.equal(s1)`.
* **获得字符串的子串**：`s.substring(2,4)`或者`s.substring(2)`,括号中是字符的索引，单独的2代表从索引为2以后开始的子串，但是（2，4）代表从索引为2字符以后开始，到索引为4字符之前。
* **寻找字符串中的字符**：`s.indexOf(c)`或者`s.indexOf(c,n)`或者`s.indexOf(s1)`。括号中只有字符c代表找到字符串中c字符所在位置的索引。（c，n）表示从n位置开始寻找c字符，s1为字符串变量，（s1）能找到字符串s1所在的位置。还可以从右边开始找`s.lastIndexOf(同普通的)`.
## 强制类型转换

* Java同c语言一样，有很多隐式转换。例如整型在某些条件下会自动转为浮点型。
* 但是浮点型不会自动转换为整型。我们可以进行强制类型转换。例如：`int a = (int)(32 /5 .0)`。

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
* 与c语言一样，Java中也有`do-while`循环，这个循环至少执行一次。

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
* **for-each**循环：形如:`for (int i : numbers){}`,意思是每一次循环，一次将数组numbers中的元素值赋给变量i。常用于遍历数组。 示例：
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

* **类**：定义同一类事物。（类的第一个字母要大写）类定义示例：
```java
public class Hero {
     
    String name; //姓名
     
    float hp; //血量
     
    float armor; //护甲
     
    int moveSpeed; //移动速度
}
```
* **对象**：类就像是一个模板，根据这个模板可以创建很多同一类的东西，这些根据类创建出来的东西就是对象。对象创建示例:
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
* **属性**：类中定义的变量就是类的属性，类中的属性就像一种东西的各种属性。属性可以是基本类型（如int等）也可以是类类型（如String等）.属性名称一般是小写，但是如果由两个及以上单词组成，则从第二个单词开始，首字母大写。
*  **方法**：类中的东西不仅具有属性，它还会做事情，能做的事情就是类中的方法。（方法的实质是在类中定义的函数）.方法的命名方法与属性一样。方法与属性的调用方法都是通过在对象后使用`.`。示例：
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

## 引用

* 不是基本类型而是类类型的变量，又叫做**引用**。
* 对象的创建时用`new Hero()`,但是创建的对象需要一个变量来接收才能使用，于是`Hero h = new Hero()`，此时的`=`不再是对于基本类型的赋值的意思，而是**指向**的意思。这个Hero类型的变量h就又叫做引用。（用c语言指针的概念来理解：就是h指向刚创建的Hero对象，但是Java中没有指针这个概念，所以只是一种理解）
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

* 如果另一类东西有已经定义的某一类东西全部属性，则可以通过继承来避免属性的重复定义。继承是通过关键字`extends`来实现的。示例：
```java
public class Item {
    String name;
    int price;
}

// 非继承的写法
public class Weapon{
    String name;
    int price;
    int damage; //攻击力
 
}
//继承的写法

public class Weapon extends Item{ // 通过extends来
    int damage; //攻击力
     
    public static void main(String[] args) {
        Weapon infinityEdge = new Weapon();
        infinityEdge.damage = 65; //damage属性在类Weapon中新设计的
         
        infinityEdge.name = "无尽之刃";//name属性，是从Item中继承来的，就不需要重复设计了
        infinityEdge.price = 3600;
         
    }
     
}
```

## 方法重载

* 方法重载指的是方法名一样，但是参数不一样。每次调用该名字的方法时，会自动根据对应的参数类型以及数量来调用对应的方法。示例：
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
* **构造方法（构造器）**：实例化是通过调用构造方法来实现的。构造方法同其他方法一样具有一样具有参数和语句体，但是没有返回类型。构造方法不是成员方法，不能用对象来调用它。**构造方法的名字与类的名字一样**，包括大小写也一样。示例：
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
* 如果在定义类中没有对构造方法的定义，则编译器在编译时会自动给类加上一个无参的，语句体为空的构造方法。
* 构造方法是通过`new`来调用的，如果使用的是没有参数的构造方法，则直接是`new <类名>()`来调用，如果有参数则需加上参数列表`new <类名>(参数列表)`，另外，构造方法与普通方法一样，是可以进行方法重载的。示例：
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

## 包

* 把具有某种关系的类放在一个包里。包必须在类最开始的地方声明。示例：
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
* 同一个包里的其它类可以直接使用，但是其他包里的类必须使用`import`来导入。示例：
```java
package charactor;
 
//Weapon类在其他包里，使用必须进行import
import property.Weapon;//格式为 import <包名>.<类名>;
 
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
## 成员变量的修饰符

### 类之间的关系

* 自身：指的是当前类自己。
* 同包子类：当前类的处于同一包下的子类。
* 不同包子类：当前类的没有处于同一个包下的子类。
* 同包类：两个处于一个包下，但是彼此没有继承关系的类。
* 其他类：没有处于同一个包下，也没有继承关系的两个类。


### private

* 使用private修饰的变量，只有只有这种类的对象才可以访问，子类不可以继承，其它的类就更不能访问了。

### 没有修饰符

* 没有修饰符的成员变量，自身的对象可以访问，同包的类可以访问，同包子类可以继承，不同包子类也可以继承，但是不同包的类不可以访问。

### proteced

* 使用protected修饰的成员变量，同包类可以访问和继承，不同包的类不可以访问和继承。

### public

* 任何地方，都可以访问和继承。

## 类属性（static）

* 当类中的属性被static修饰时，这个属性就叫做**类属性**，又叫做**静态属性**。如果某个属性被声明为类属性，那么该类所有的对象都共享这个值。
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
            
           Hero.copyright = "版权由Riot Games公司所有";
            
           System.out.println(garen.name);
           System.out.println(garen.copyright);
            
           Hero teemo =  new Hero();
           teemo.name = "提莫";
           System.out.println(teemo.name);    
           System.out.println(teemo.copyright);
         
    }
     
}
* 对类属性的赋值通过直接使用类名来完成`Hero.copyright = `.但是在实际的使用中（如idea）虽然使用对象名来改变不被

