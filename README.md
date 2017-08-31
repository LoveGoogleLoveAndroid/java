# java
java basic.

`《Java核心技术卷一》笔记`


  
    
      
      
## Java关键术语：
简单性（语法是C++的纯净版本，无头文件、指针、结构、联合、操作符重载、虚基类）、面向对象、网络技能、健壮性、安全性、可移植性、解释性、高性能、多线程
源代码的文件名必须与公有类的名字相同  
Java所有的方法必须是某个类的方法，包括main函数  
 
## 注释：
比C++多了文档注释/**   */  
 
##  基本数据类型：
byte（1）、short（2）、int（4）、 long（8）、float（4）、double（8），char（1）、boolean（1），无无符号类型；整型值和布尔型不能相互转换
 
## 声明与定义：
java中不做区分  
 
## 字符串：
```
String greeting = “hello”;         // greeting更像是C++里面的指向常量的指针
greeting = greeting.substring(0, 3) + “p!”   // help!  
```
String为不可变字串，实际将greeting 指向另一个字符串，意味着堆中有两个字符串”hello”和”help!”；字符串+连接像是C++里面对String重载了+操作符  
优点：编译器可以让字符串共享；Java设计者认为共享带来的高效率远胜提取、拼接字符串带来的低效率；可以用StringBuilder防止既耗时又费空间的链接操作
```
StringBuilder builder = new StringBuilder();
builder.append(ch);
builder.append(str);
String completedString = builder.toString();
 
int compareTo(String other);   // 按字典顺序比较字符串
boolean equals(Object other); // 比较两个对象的值
==  // 比较两个对象的地址
```
 
## 块作用域：
C++中可以在块中重定义同名变量，且会覆盖外层变量，Java中不允许这样做  
 
## 循环：
Java中不支持goto，但是可以通过break加标签的形式跳出多层循环；不止循环，标签可用到任何语句中  
```
Label:
{
         If (condition)
                   break Lable；
}
 
for( variable:collection ) statement;
```
collection必须是一个数组或者是实现了Iterable接口的类对象（如ArrayList）
 
 
## 类之间关系：
继承（is-a）、实现（implements）、聚合（has-a）、组合、依赖（uses-a）、关联  
 
## 对象：
Java中的对象变量（或者叫对象引用）与C++中的引用不同，C++中没有空引用，而且引用不能被赋值，它更像是C++中的对象指针
`Date birthday;  // java`  
等同于：
`Data * birthday; // C++`  
 
## 构造器：
与类名相同、每个类可以有多个构造器、可以有任意类型和个数的参数，但是无返回值、在创建对象的时候由系统调用，不能手动调用  
 
## 私有方法：
有时候一个计算代码有若干个辅助方法，这些辅助方法不应该成为共有接口的一部分；或者需要一个特别的调用次序，只有最先调用的接口可设计为公有接口  
 
## final实例域：
final大多应用于基本数据类型或不可变类对象（如果类中的每个方法都不会改变其对象，就是不可变的类）；对于可变类，用final修饰会误导读者  
```
private final Date hireDate;  // 即C++的常指针，一旦初始化，无法指向其他对象
```

## 静态域：
静态变量使用不多，静态常量使用很多  
```
public class Math
{
         public static final double PI=3.1415926;
}
public class System
{
         public static final PrintStream out = …;
}
```

## 静态方法：
无this指针，只可访问静态域  
两种常用场景：一个方法无需访问对象状态或只需访问静态域  
 
static的前世今生：  
1. 最早用作C里面标识局部变量的存储属性，对比auto
2. 重用在C里面修饰全局变量和函数，修改其访问属性，对比extern
3. C++中表示不属于对象而属于整个类的变量和函数
4. Java中含义与C++完全相同
 
## 参数传递：
值传递；C++除了值传递，还有引用传递；Java中的对象引用类似于C++的对象指针传递  
 
## 方法签名：
返回类型不是方法签名的一部分，即不能有两个同名，参数类型也相同却返回类型不同的方法  
 
## 初始化顺序：
1. 类中域系统会默认初始化，数值为0，布尔false，对象引用null，但是局部变量不会
2. 按照声明次序执行类中域赋值语句（C++中不能直接初始化实例域，所有的域必须在构造器中初始化，但是有一个初始化列表的语法可以进行设置）和初始化块（静态初始化块早于普通初始化块）
3. 如果构造器调用了第二个构造器，则执行第二个构造器
4. 执行这个构造器
 
## 构造函数：
如果类中提供了至少一个构造器，但是没有提供默认的构造器（即无参构造器），则在创建对象时如果没有提供构造参数会被视为不合法（仅当类中没有提供任何构造器的时候，系统才会提高一个默认的构造器）  
 
## this指针：
1. 做隐形参数（同C++）
2. 用于调用另一个构造器（C++中不允许在一个构造器里调用另一个）
```
Public Employee(double s)
{
         this(“Employee #” + nextId, s);
         nextId++;
}
```

## super关键字：
1. 调用超类的方法
2. 调用超类的构造器（C++则采用作用域标识符：：）
 
 
## 析构器：
Java不支持，但可以为任何类添加finalize方法，在垃圾回收清除对象之前调用，不能依赖他回收任何稀缺的资源，应该由人工管理  
 
## 包：
从编译器的角度看，嵌套的包之间没有任何关系，如java.util和java.util.jar  
如何没有制定任何访问修饰符，则默认为包作用域，可被包中所有方法访问  
 
## 类的定义格式：
* public部分 
* 包作用域部分 
* private部分

## 每个部分定义顺序：
* 实例方法 
* 静态方法 
* 实例域 
* 静态域
 
## 多重继承：
Java用extends关键字代替了C++的:；而且跟C++不同，Java中不支持多重继承，而且所有的继承都是public继承  
 
## 动态绑定：
1. Java的默认处理方式，如果希望一个方法不具有虚拟特征，可标记为final；C++默认是静态绑定
2. 返回类型并不是签名的一部分，在覆盖方法时，一定要保证返回类型的兼容性，子类覆盖方法的返回类型必须与父类一样，或者是其子类型，而且子类方法的可见性不能低于父类，如父类中为public，则子类也必须是public
3. 静态绑定的方法：private方法、static方法、final方法和构造器，因为编译器可以准确的知道调用的是哪个方法
4. final类（其中的方法自动为final，但不包括域）可阻止继承，final方法可阻止覆盖

C++中没有阻止覆盖的方法，但是有阻止继承的技巧  
 
## 强制类型转换：
1. 唯一原因是在暂时忽略了对象的实际类型后可以使用对象的全部功能
2. 将子类引用赋给父类引用可以，反之必须进行强制类型转换
3. 只能在继承层次进行类型转换
4. 将父类转换为子类前，应该使用instanceof进行类型检查
 
## 抽象类：
1. 为了提高程序的清晰度，包含一个或多个抽象方法的类必须声明为抽象的，关键字abstract，C++中无专门的关键字
2. 抽象类可以包括具体数据和方法
3. 即使类中不含抽象方法，也可声明为抽象类
4. 抽象类不能实例化，但是可以创建抽象类的对象变量
 
## protected：
java中其作用域是派生类和整个包，而C++中只有派生类可访问  
 
## Object：
1. 只有基本类型不是对象，所有的数组类型都扩展于Object类；C++没有根基，但是每个指针都可以转换为void *
```
Object obj = new int[10];
```
2. equals方法的标准写法
```
public boolean equals( Object otherobj )
{
        If ( this == otherObj )       return true;
         If ( otherObj == null )       return false;
         If ( getClass() != otherObj.getClass() )    return false;
         Employee other = (Employee)otherObj;
 
         return ( name.equals(other.name) && salary == otherObj.salary && hireDay.equals( OtherObj.hireDay );
 
}
```
3. hashCode方法必须与equals的定义一致，如果重新定义equals方法，则必须重新定义hashCode方法，每个对象默认的散列码是其存储地址
4. toString方法用于返回表示对象值的字符串，只要对象与一个字符串通过操作符+连接，就会自动调用该方法，以获取这个对象的字符串描述
 
## 对象包装器：
所有的基本类型都有一个与之对应的类，这些类称为包装器  
Integer Long Float Double Short Byte Character Void Boolean（前六个派生于Number）,对象包装器是不可变的，还是final，因此不能定义它们的子类，尖括号内的不允许是基本类型  
`ArraryList<Integer> list = new ArrayList<Integer>();`  
ArrayList<Integer>的效率要远低于int[]数组，适合构造小型集合，程序猿操作的方便性要比执行效率更加重要  

## 自动打包：
`list.add(3)`将自动变换为`list.add(new Integer(3));`  
## 自动拆包：
`int n = list.get(3)`将自动变换为`int n = list.get(3).intValue();`  
## 字符串转为整型：
```
int x = Integer.parseInt(s);
Integer y = Integer.valueOf(s);
int z = Integer.valueOf(s).initValue();
``` 
## 整型转为字符串：
```
String s = String.valueOf(i);
String s = Integer.toString(i);
String s = "" + i;
``` 
修改参数值的方法：使用IntHolder、BooleanHolder等

## 反射：
1. 在程序运行期间，Java运行时系统始终为所有的对象维护一个被称为运行时的类型标识，这个信息保存着每个对象所属的类足迹，保存这些信息的类被称为Class
2. 
```
a：Employee e;
Class cl = e.getClass()
b：String className = “java.util.Date”;
Class cl = Class.forName(className);
c：Class cl = Date.class;          // int.Class; Double[].Class
```
3. 反射很脆弱，编译器很难帮助人们发现程序中的错误，任何错误只能在运行时被发现
4. java.lang.reflect有三个类，`Field、Method、Constructor
getFields、getMethods、getConstructors`分别返回类提供的public域、方法和构造器，
其中包括超类的公有成员
`getDeclareFields、getDeclareMethods、getDeclareConstructors`分别返回类提供的public域、方法和构造器，其中包括私有和受保护的成员，但不包括超类的成员  
`getModifiers`：返回描述构造器、方法或域的修饰符  
`getName`：返回构造器、方法或域的名字  
`getParametertypes`：构造器和方法参数列表  
`getRetureType`：方法返回类型  
 
## 接口：
1. 所有方法默认为public（所以实现接口时必须声明为public），所有域默认为public static final
2. 接口不是类，不能实例化，但是可以声明接口的变量
```
x = new Comparable(…); //error
Comparable x;          //ok
```
3. 接口可以被扩展（继承）
```
public interface Moveable
{
         void move(double x, double y);
}
public interface Powered extends Moveable
{
         double milesPerGallon();
}
```
4. 标记接口：Cloneable、Serializable、RandomAccess、Remote，其唯一目的是可以用instanceof 进行类型检查
5. 在任何使用C++函数指针的地方，都应该考虑使用Java中的接口
```
public interface Comparable<T>
{
         int compareTo(T other);
}
```

## 对象克隆：
1. Object默认的clone方法，只能将各个域进行相应的拷贝
2. 如果类中仅含有基本数据类型和不可变对象引用，则浅拷贝不会产生任何问题，如果类中存在可变的对象引用，则必须重新定义clone方法，以便实现深拷贝
3. 默认的clone方法是否满足要求？默认的clone方法是否能够通过调用可变对象的clone得到修补？是否不应该使用clone？
4. 即使clone的默认实现即浅拷贝可以满足要求，也应该实现Cloneable接口，将clone方法定义为public，并调用super.clone()
5. 所有的数组类型包含一个public的clone方法
```
int[] luckyNumber = {1, 3, 5, 7, 9};
int[] clone = (int[])luckyNumber.clone();
```

## 内部类：
1. 内部类可以访问该类定义作用域中的数据，包括私有；可以对同一个包中其他类实现隐藏；当想定义一个回调函数且不想编写大量代码，使用匿名内部类；内部类类似于C++的嵌套类
2. 编译器会为内部类生成一个默认的构造器（传一个外部类对象引用的参数），以把内部类和其外部类连接起来
3. 内部类可以是私有类，常规类只可以是包可见或public
4. 如果内部类只使用一次，则可将其定义在方法内，形成局部类，对外部世界完全隐藏；不能用public或private修饰，其作用域仅在方法内；可以访问局部变量，但只能是final，如果要在内部类更新某个数据，可以考虑定义只有一个数据的数组，如
`final int[] counter = new int[1];  `        // counter是对象引用，不可引起地方对象，但其所引用的对象counter[0]可以设置
5. 如果只创建这个类的一个对象，则无需命名了，可定义为匿名内部类，构造器名必须与类名相同，所以匿名内部类没有构造器
```
new SuperType( construction parameters )
{
         inner class methods and data
}
```
SuperType可以是接口，也可以是一个类  
6. 有时候使用内部类只是为了把一个类隐藏在另一个类的内部，并不需要内部类引用外围类对象，可以将内部类定义为static静态内部类，以便取消产生的引用
7. 定义在接口中的内部类自动为static和public
 
## 异常分类：
Throwable:：Error（系统内部错误和资源耗尽，应终止程序）和Exception  
Exception：RuntimeException（程序错误导致的，一定是你的问题，如错误的类型转换，数组越界，空指针等）和IOException  
`Error和RuntimeException`称为未检查异常，其他为已检查异常；程序应该声明所有尽可能的已检查异常，而未检查异常要么不可控（Error），要么就应该避免发生（RuntimeException）  
Java中，只能抛出Throwable子类的对象，而C++可以抛出任何类型的值
 
## 捕获异常：
如果在try中任何代码抛出一个在catch说明的异常类，那么：  
1. 程序将跳过try语句块的其余代码
2. 执行catch的代码
如果在try没有抛出异常，则跳过catch代码  
如果抛出没有在catch声明的异常，则退出方法  
应该捕获那些知道如何处理的异常，不知道如何处理，应该将其传递出去，在方法的首部添加一个throws说明符，以便告知方法可能会抛出异常
可以在catch中继续抛出异常，这么做的目的是改变异常的类型  
Java中没有析构器，需要手工回收代码，写入finally子句  
```
InputStream in = …
try
{
       try
       {
                   code that might throw exception
         }
         finally
         {
                   in.close();
        }
}
catch ( IOException e)
{
         show error dialog
}
``` 
 
## 断言：
允许在测试期间向代码插入一些检查语句，当代码发布时，这些语句会被移除  
```
assert condition;
or
assert condition : expression
```
若结果为false，则抛出AssertionError异常  

## Java三种处理系统错误的机制：
`异常、日志、断言 `
断言失败是致命的，不可恢复的错误，是在测试阶段调试的战术性工具，日志记录是在程序的整个声明周期都可以使用的策略性工具
 
## 泛型：
使用泛型机制编写的代码要比那些杂乱的使用Object变量，然后再进行强制类型转换的代码具有更好的安全性和可读性  
Java的泛型类类似于C++的模版类，只是没有专用的template关键字  
 
## 类型变量：
```
public static Pair<String> minmax(String[] a)
{
         if ( a == null || a.length == 0 )  return null;   
         String min = a[0]; max = a[0]; 
         for (int i=0; i<a.length; i++)
         {
                   if ( min.compareTo(a[i]) > 0 ) min = a[i];
                   if ( max.compareTo(a[i]) < 0 ) max = a[i];
         }
         
        return new Pair<String>(min, max);
}
```

## 类型变量限定：
```
public static <T> T min(T[] a)
{
         if (a == null || a.length == 0)  return null;
         T small = a[0];
         for (int i=0; i<a.length; i++)
         {
                   if (small.compareTo(a[i]) > 0) small = a[i];
         }
         return small;
}
public static <T extends Comparable> T min(T[] a)….
```
限定中最多有一个类，可以有多个接口：`T extends Comparable & Serializable`  
无论何时定义一个泛型类型，都会自动提供一个相应的原始类型，是删去类型参数后的泛型类型名，用第一个限定的类型变量来替换，如果没有限定就用Object替换  
C++中不能对模版参数的类型加以限制，每个模版实例化产生不同的类型，这一现象称为“模块代码膨胀”，Java中不存在这个问题  
 
## 约束与局限性
1. 不能用类型参数代替基本类型，没有Pair<double>，只有Pair<Double>
2. 运行时类型查询只适用于原始类型
3. 不能抛出或捕获泛型类实例，不能在catch中使用类型变量，但可以在异常声明中使用
4. 参数化类型的数组不合法Pair<String>[] table = new Pair<String>[10]; ERROR
5. 不能实例化类型变量，不能使用new T(…)，new T[…]或T.clsss；Class类是泛型的，如String.class实际上是一个Class<String>类的对象，事实上也是唯一的对象
6. 不能在静态域或方法中引用类型变量  
 
## 泛型类型的继承规则：
无论S和T是什么关系，通常，Pair\<S\>与Pair\<T\>没有什么联系  
```
Pair<Manager> managerBuddies = new Pair<Manager>(ceo, cfo);
Pair<Employee> employeeBuddies = managerBuddies; // illegal;
 
Manger[] managerBuddies = {ceo, cfo};
Employee[]employeeBuddies = managerBuddies; // ok
```  

## 通配符类型：
固定的泛型类型系统使用起来并没有那么令人愉快  
`Pair< ? extends Employee> `              // Employee是?的上界
表示任何泛型的Pair类型，其类型参数是Employee的子类，如Pair<Manager>，而不是Pair<String>
 
## 通配符限定：
```
Pair<? super Manager>            // Manager是?的下界
 
public interface Comparable<T>
{
         public int compareTo(T other);
}
public static <T extends Comparable< ? super T>>  T min(T[] a)  // 看起来很吓人
```

## 集合类：
是带有类型参数的泛型类，不允许有重复的对象  
``` 
public interface Collection<E>
{
         boolean add( E element );        // 集合变化返回true，否则返回false
         Iterator<E> iterator();
        
         int size();
         boolean contains( Object obj );
         boolean equals( Object other );
         boolean remove( Object obj );
…
}
 
public interface Iterator<E>
{
         E next();
         boolean hasNext();
         void remove();
}
 
Collection<String> c = …;
Iterator<String> iter = c.iterator();
for ( String element : c )   // foreach可以与任何实现了Iterable接口的对象一起工作
{       
}
public interface Iterable<E>
{
         Iterator<E> iterator();
}
 
Collection<String> c = …;
Iterator<String> iter = c.iterator();
iter.next();        // skip over the first element
iter.remove();  // now remove it
remove之前必须调用next方法，否则抛出IllegalStateException异常
```

## 链表：
Java中的链表都是双向链表，有序集合  
LinkedList：任何位置高效插入删除的有序序列  
```
List<String> staff = new LinkedList<String>();  
staff.add(“Amry”);
staff.add(“Bob”);
staff.add(“Carl”);
Iterator iter = staff.iterator();          // Iterator中没有提供add方法
String first = iter.next();            // visit the first element
String second = iter.next();      // visit the second element
iter.remove();           //      remove the second element
 
interface ListIterator<E> extends Iterator<E>
{
         void add( E element );      // 与Collection.add不同，它假定总会改变链表
         void set( E element );
         boolean hasPrevious();
         …
}
 
ListIterator<String> iter = staff.listIterator();
iter.next();        // skip past the first element
iter.add(“Juliet”)                // Amry->Juliet->Bob->Carl
 
ListIterator<String> iter = staff.listIterator();
String old = iter.next();     // return the first element
iter.set(netValue);            // sets first element
```
若有两个迭代器，一个更改，另一个遍历，则会出错  
 
不应该使用这种让人误解的随机访问方法来遍历链表：  
```
for (int i=0; i<list.size(); i++)
{
         do something with list.get(i);
}
```

## 数组列表：
`ArrayList`：动态增长或缩减的索引序列，封装了一个动态再分配的对象数组；非线程安全  
`Vector`：所有方法都是同步的，线程同步操作将会耗费大量的时间
 
## 散列集：
Java中的散列集通过链表数组实现  
`set`：没有重复元素的集合  
`HashSet`：  
```
Set<String> words = new HashSet<String>();
words.add(“Hello”);
words.add(“world!”);
 
Iterator<String> iter = words.iterator();
String first = iter.next();
``` 

`TreeSet`：树集是有序集合  
```
SortedSet<String> sorter = new TreeSet<String>();
sorter.add(“Bob”);
sorter.add(“Army”);
sorter.add(“Carl”);
for (String s : sorter)       System.out.println(s);      // 自动排序 Army->Bob->Carl
```

`Linked 改快读慢；Array 读快改慢；Hash 两都之间`
 
`Collection是集合接口`  
    |————`Set子接口`：无序，不允许重复  
    |————`List子接口`：有序，可以有重复元素  
    `Set`：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变  
    `List`：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变  
    
`Set和List具体子类`  
    `Set`  
     |————`HashSet`：以哈希表的形式存放元素，插入删除速度很快  
|————`TreeSet`：红黑树  
    `List`  
     |————`ArrayList`：动态数组  
     |————`LinkedList`：链表、队列、堆栈  
    `Vector`是一种老的动态数组，是线程同步，效率很低，一般不赞成使用  
 
`Iterator`：只能正向遍历集合，适用于获取移除元素  
`ListIerator`：继承Iterator，可以双向列表的遍历，同样支持元素的修改

this should be a table for the difference of above...  

## 线程与进程差别：
进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动，是系统进行资源分配和调度的一个独立单位  
线程是进程的一个实体, 是CPU调度和分派的基本单位，它是比进程更小的能独立运行的基本单位，线程自己基本上不拥有系统资源，只拥有一点在运行中必不可少的资源(如程序计数器，一组寄存器和栈)，但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源  
进程和线程的主要差别在于它们是不同的操作系统资源管理方式：进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程  
进程只能在一个时间干一件事，如果想同时干两件事或多件事，进程就无能为力了，进程在执行的过程中如果阻塞，例如等待输入，整个进程就会挂起，即使进程中有些工作不依赖于输入的数据，也将无法执行  
因为要并发，发明了进程，又进一步发明了线程；只不过进程和线程的并发层次不同：进程属于在处理器这一层上提供的抽象；线程则属于在进程这个层次上再提供了一层并发的抽象。如果我们进入计算机体系结构里，就会发现，流水线提供的也是一种并发，不过是指令级的并发。这样，流水线、线程、进程就从低到高在三个层次上提供我们所迫切需要的并发；不要调用Thread或者Runnable对象的run方法；直接调用run方法，只会执行同一线程中的任务，而不会启动新线程  
``` 
void interrupt();        // 向线程发送中断请求，线程的中断状态被设置为true，如果线程目前被sleep调用阻塞，InterruptedException异常抛出
static boolean interrupted();   // 测试当前线程（执行此语句的线程）是否被中断，并将线程中断状态重置为false
boolean isInterrupted();           // 测试当前线程（执行此语句的线程）是否被中断
static Thread currentThread();        // 返回当前执行线程的Thread对象
void join;  // 等待终止指定的线程
void stop();                // 过时
void suspend();         // 过时
void resume();          // 过时
```

## 线程状态：
```
New：创建一个线程如new Thread()
Runnable：开始一个线程如thread.start()，可能运行，也可能没有运行，处于可运行状态
Blocked：当一个线程试图获取一个内部的对象锁，而该锁被其他线程持有则进入阻塞状态
Waiting：当一个线程等待另一个线程通知调度器一个条件时，进入等待状态
Timed waiting：计时等待
Terminated：run方法正常退出或没有捕获的异常终止了run方法而意外死亡
```

## 守护线程：
`thread.SetDaemon();       // 唯一用途是为其他线程提供服务`  
如果只剩下守护线程，就没必要运行程序了，守护线程应该永远不访问固有资源，如文件数据库，它会在任何时候甚至在一个操作的中间发生中断  
 
## 重入锁：
重入锁（ReentrantLock）是一种递归无阻塞的同步机制，它不是synchronized的简单替代，看起来 ReentrantLock 无论在哪方面都比 synchronized 好；所有 synchronized 能做的，它都能做，它拥有与synchronized 相同的内存和并发性语义，还拥有 synchronized 所没有的特性，在负荷下还拥有更好的性能；一般来说，除非您对 Lock 的某个高级特性有明确的需要，或者有明确的证据（而不是仅仅是怀疑）表明在特定情况下，同步已经成为可伸缩性的瓶颈，否则还是应当继续使用 synchronized；synchronized 仍然有一些优势，比如在使用 synchronized 的时候，不能忘记释放锁；在退出 synchronized 块时，JVM 会为您做这件事。您很容易忘记用 finally 块释放锁，这对程序非常有害，您的程序能够通过测试，但会在实际工作中出现死锁，那时会很难指出原因；另一个原因是当 JVM 用 synchronized 管理锁定请求和释放时，JVM 在生成线程转储时能够包括锁定信息，这些对调试非常有价值，因为它们能标识死锁或者其他异常行为的来源，而Lock 类只是普通的类，JVM 不知道具体哪个线程拥有 Lock对象；在确实需要一些 synchronized 所没有的特性的时候，比如时间锁等候、可中断锁等候、无块结构锁、多个条件变量或者锁投票可以使用重入锁  
解锁操作必须放在finally内，如果在临界区的代码抛出异常，锁必须被释放；必须留心临界区的代码，不要因为异常的抛出而跳出了临界区这样finally虽然执行，但是对象可能处于一种受损状态  
```
public void transfer( int from, int to, int amount )
{
         bankLock.lock();
         try
         {
                   accounts[from] -= amount;
                   accounts[to] += amount;         
         }
         finally
         {
                   bankLock.unlock();
         }
}
…
private Lock bankLock = new ReentrantLock  // implements the Lock interface
```

## 条件对象：
通常，线程进入临界区，却发现在某一条件满足后才能执行，要使用一个条件对象来管理那些已经获得一个锁却不能做有用工作的线程  
```
if ( bank.getBalance(from) >= amount)
         bank.transfer( from, to, amount )   // thread might be deactivated at this point
 
 
public void transfer( int from, int to, int amount )
{
         bankLock.lock();
         try
         {
                   while ( accounts[from] < amount )
                            sufficientFunds.await();           // block current thread, unlock() current thread
                   accounts[from] -= amount;
                   accounts[to] += amount;         
 
                   sufficientFunds.signalAll();       // 解除等待线程的阻塞
         }
         finally
         {
                   bankLock.unlock();
         }
}
…
private Condition sufficientFunds = bankLock.newCondition();
```
当一个线程拥有在某个条件的锁时，它仅仅可以调用await（当一个线程调用await，没有办法重新激活自身，只能寄希望于其他线程）、signalAll或signal（随机解除等待集中某个线程的阻塞状态，如果该线程不能运行，将再次阻塞，如果没有其他线程再次调用signal，系统就会死锁）  
* 锁可以保护代码片段，任何时刻只能有一个线程执行被保护的代码
* 锁可以管理试图进入被保护代码段的线程
* 锁可以拥有一个或多个相关的条件对象
每个条件对象管理那些已经进入被保护的代码段但是还不能运行的线程  
 
## synchronized：
Java为每个对象提供一个内部锁，如果一个方法用synchronized关键字声明，那么对象的锁将保护整个方法  
```
public synchronized void method()
{
}
```
等价于：
```
public void method()
{
         this.intrinsickLock.lock();
         try
         {
                   …
         }
         finally
         {
                   this.intrinsicLock.unlock();
         }
}
```
内部对象锁只有一个相关条件  
```
public synchronized void transfer( int from, int to, int amount )
{
                   while ( accounts[from] < amount )
                            wait();               // 等价于sufficientFunds.await();
                   accounts[from] -= amount;
                   accounts[to] += amount;         
 
                   notifylAll();        // 等价于sufficientFunds.signalAll();
}
```
* 内部锁不能中断一个正在试图获得锁的线程
* 内部锁不能设定超时
* 内部锁仅有单一条件，可能不够
最好既不用`Lock/Condition`也不用`synchronized`关键字，许多情况下可以用`java.util.concurrent`  
 
## 同步阻塞：
lock对象对创建仅仅用来使用每个Java对象持有的锁  
```
public void transfer( int from, int to, int amount )
{
         synchronized ( lock )
         {
                   accounts[from] -= amount;
                   accounts[to] += amount;         
         }
}
…
private Object lock = new Object();
```

## Volatile：
仅仅为了读写一个或两个实例域就进行同步，开销过大  
Java 语言提供了一种稍弱的同步机制，即 volatil，用来确保将变量的更新操作通知到其他线程，保证了新值能立即同步到主内存，以及每次使用前立即从主内存刷新；当把变量声明为volatile类型后，编译器与运行时都会注意到这个变量是共享的，volatile关键字为实例域的同步访问提供了一种免锁机制，如果声明为volatile，那么编译器和虚拟机就知道是可能被另一个线程并发更新  
如果实例域是final或volatile，或对域的访问由公有的锁进行保护，则域的并发访问是安全的  
volatile不能提供原子性，也并非线程安全  
```
public void filpDone()
{
         done = !done;  // cannot modify for sure
}
```


## 死锁：
两个或两个以上的进程在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去  
死锁原因：  
* 系统资源不足
* 进程运行推进的顺序不合适
* 资源分配不当  
死锁条件：  
* 互斥条件：进程在某一时间内独占资源
* 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
* 不剥夺条件：进程已获得资源，在末使用完之前，不能强行剥夺
* 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系  
预防死锁：  
通过设置某些限制条件，去破坏产生死锁的四个必要条件中的一个或者几个，来预防发生死锁，预防死锁是一种较易实现的方法，但是由于所施加的限制条件往往太严格，可能会导致系统资源利用率和系统吞吐量降低    
避免死锁：  
该方法同样是属于事先预防的策略，但它并不须事先采取各种限制措施去破坏产生死锁的的四个必要条件，而是在资源的动态分配过程中，用某种方法去防止系统进入不安全状态，从而避免发生死锁  
锁测试与超时：  
线程在调用lock方法获得另一个线程所持有的锁的时候，很可能发生阻塞，应该谨慎的申请锁；lock方法不能被中断，如果一个线程在等待获得一个锁时被中断，中断线程在获得锁前一直处于阻塞状态，如果出现死锁，那么，lock方法将无法终止；如果调用带有超时参数的trylock，如果线程在等待期间被中断，将抛出InterruptedException异常，允许程序打断死锁；如果一个线程被另一个线程通过调用signalAll或signal激活，或者超时时限已到，或者线程被中断，那么await方法将返回  
## 读写锁：
如果很多线程从一个数据结构读取数据而很少线程修改其中数据，可允许对读者线程共享访问，对写者线程互斥访问
```
private ReetrantReadWriteLock rwl = new ReetrantReadWriteLock();
private Lock readLock = rwl.readLock();
private Lock writeLock = rwl.writeLock();
```
为什么弃用stop和suspend方法：  
stop和suspend有个共同点：都试图控制一个给定线程的行为；stop天生就不安全，经验证明经常导致死锁，它用来终止未结束的方法，如run方法，线程被终止，立即释放被它锁住的对象的锁，导致对象处于不一致状态，当线程要终止另一个线程时，无法知道什么时候调用stop是安全的，什么时候会导致对象被破坏；suspend不会破坏对象，但是，如果用suspend挂起一个持有一个锁的线程，那么该锁在恢复之前不可用，如果调用suspend方法的线程试图获得同一个锁，那么程序死锁，被挂起的线程等着被恢复，而将其挂起的线程等待获得锁  
## 阻塞队列：
对于许多线程问题，可以通过使用一个或多个队列以优雅且安全的方式将其形式化；生产者线程向队列插入元素，消费者线程则取出它们；使用队列，可以安全的从一个线程向另一个线程传递数据；当试图向队列添加元素而队列已满，或是想从队列移除元素而队列为空的时候，阻塞队列导致线程阻塞；在协调多个线程之间的合作时，阻塞队列是一个有用的工具；工作者线程可以周期性的将中间结果存储在阻塞队列，而其他的工作者线程移出中间结果并进一步加以修改，队列会自动的平衡负载  
```
add()         队列满则抛出IllegalStateException异常
remove()  移出并返回对头元素，队列空则抛出NoSuchElementException异常
element()  返回对头元素，队列空则抛出NoSuchElementException异常
offer()  添加一个元素，如果队列满则返回false
peek()  返回对头元素，如果队列空则返回null
poll()   移除并返回对头元素，如果队列空则返回null
put()   添加一个元素，如果队列满，则阻塞
take()  移除并返回对头元素，如果队列空，则阻塞
LinkedBlockingQueue：链表，容量无上界
LinkedBlockingDeque：链表，双端队列
ArrayBlockingQueue：数组，需要指定容量
PriorityBlockingQueue：链表，优先级队列
```

## 高效的散列、集合和队列：
`ConcurrentHashMap、ConcurrentSipListMap、ConcurrentSkipListSet、ConcurrentLinkedQueue`  
这些集合使用复杂的算法，通过允许并发的访问数据结构的不同部分来使竞争最小化  
Vector和Hashtable类提供了线程安全的动态数组和散列表的实现，被ArrayList和HashMap取而代之，这些类不是线程安全的，可以通过同步包装器变成线程安全的  
## Callable和Future：
创建线程的2种方式，一种是直接继承Thread，另外一种就是实现Runnable接口；这2种方式都有一个缺陷就是：在执行完任务之后无法获取执行结果；如果需要获取执行结果，就必须通过共享变量或者使用线程通信的方式来达到效果，这样使用起来就比较麻烦；自从Java 1.5开始，就提供了Callable和Future，通过它们可以在任务执行完毕之后得到任务执行结果  
Runnable封装了一个异步执行的任务，可以把它想象成为一个没有参数和返回值的异步方法；Callable与Runnable类似，但是有返回值，只有一个方法：  
```
public interface Callable<V>
{
         V call()  throws Exception;
}
```
Future保存异步计算的结果，可以启动一个计算，将Future对象交给某个线程，然后忘了它；Future对象的所有者在结果计算好之后可以获得它  
```
public interface Future<V>
{
         V get() throws…; // 调用被阻塞，直到计算完成
         V get( long timeout, TimeUnit unit ) throws…; //
         void cancel( Boolean mayInterrupt ); //
         boolean isCanceled();      //
         Boolean isDone();    // 计算完成后返回true
}
```
FutureTask包装器是一种非常便利的机制，可以将Callable转换为Future和Runnable  
```
Callable<Integer> myConputation = …;
FutureTask<Integer> task = new FutureTask<Integer>(myConputation);
Thread t = new Thread(task);           // it’s Runnable
t.start();
…
Integer result = task.get();      // it’s Future
```
## 线程池：
创建一个新的线程要涉及到与操作系统的交互，有一定代价；如果程序中创建了大量生命期很短的线程，应该使用线程池；一个线程池中包含许多准备运行的空闲线程，将Runnable对象交给线程池，就会有一个线程调用run方法，当run退出时，线程不会死亡，而是在池中准备为下一个请求服务；另一个使用线程池的理由是减少并发线程的数目  
```
newCachedThreadPool   必要时创建线程，空闲线程保留60s
newFixedThreadPool        固定数量线程，一直保留
newScheduledThreadpoll         用于预定执行而构建的线程池，替换timer
newSingleThreadExecutor       只有一个线程的池，顺序执行每个提交任务
newSingleThreadScheduledExecutor       用于预定执行而构建的单线程池
```
它们返回实现了ExecutorService接口的ThreadPoolExecutor类的对象  
```
Future<?> submit( Runnable task )
Future<T> submit( Runnable task, T result )
Future<T> submit( Callable<T> task )
```
当用完一个线程池的时候，调用shutdown，启动该线程池的关闭序列，不再接受新的任务，当所有任务都完成后，线程池的线程死亡  
使用线程池应该做的事：  
* 调用Executors类中的静态方法newCachedThreadPool或newFixedThreadPool  
* 调用submit提交Runnable或Callable  
* 如果想取消一个任务，或如果提交Callable对象，就要保存好返回的Future对象  
* 当不再提交任何任务时，调用shutdown    
## 信号量：
`Semaphore`：允许线程集等待直到被允许继续运行为止，限制资源的访问总数，如果许可数是1，常常阻塞线程直到另一个线程给出许可为止  
建议在信号量的行为能适合你面对的同步问题时才能使用它，否则会陷入到思维的混乱  
## 倒计时门栓：
`CountDownLatch`：允许线程集等待直到计数减为0，当一个或多个线程需要等待直到指定数目的事件发生  
```
public class CountDownLatchTest {
    // 模拟100米赛跑，10名选手已经准备就绪，只等裁判一声令下。当所有人都到达终点时比赛结束
    public static void main(String[] args) throws InterruptedException {      
        final CountDownLatch begin = new CountDownLatch(1);  // 开始的倒数锁  
        final CountDownLatch end = new CountDownLatch(10);  // 结束的倒数锁       
        final ExecutorService exec = Executors.newFixedThreadPool(10);   // 十名选手
        for (int index = 0; index < 10; index++) {
            final int NO = index + 1; 
            Runnable run = new Runnable() {
                public void run() { 
                    try {                        
                        begin.await();  // 如果当前计数为零，则此方法立即返回，否则等待
                        Thread.sleep((long) (Math.random() * 10000)); 
                        System.out.println("No." + NO + " arrived"); 
                    } catch (InterruptedException e) { 
                    } finally {                        
                        end.countDown();       // 每个选手到达终点时，end就减一
                    } 
                } 
            }; 
            exec.submit(run);
        } 
        System.out.println("Game Start"); 
        // begin减一，开始游戏
        begin.countDown(); 
        // 等待end变为0，即所有选手到达终点
        end.await(); 
        System.out.println("Game Over"); 
        exec.shutdown(); 
    }
}
```
## 障栅：
`CyclicBarrier`：允许线程集等待直到其中预定数目的线程到达一个公共障栅，然后可以选择执行一个处理障栅的动作；当大量的线程需要在它们的结果可用之前完成时；障栅是循环的，可以在所有等待线程被释放后被重用，有别于CountDownLatch，只能被使用一次；需要所有的子任务都完成时，才执行主任务，这个时候就可以选择使用CyclicBarrier，在所有参与者都已经在此 barrier 上调用 await方法之前，将一直等待，如果当前线程不是将到达的最后一个线程，出于调度目的，将禁用它  
```
public class CyclicBarrierTest {
         public static void main(String[] args) throws IOException, InterruptedException {
                  //如果将参数改为4，但是下面只加入了3个选手，这永远等待下去
                   //Waits until all parties have invoked await on this barrier.
                   CyclicBarrier barrier = new CyclicBarrier(3);
                   ExecutorService executor = Executors.newFixedThreadPool(3);
                   executor.submit(new Thread(new Runner(barrier, "1号选手")));
                   executor.submit(new Thread(new Runner(barrier, "2号选手")));
                   executor.submit(new Thread(new Runner(barrier, "3号选手")));
                   executor.shutdown();
         }
}
class Runner implements Runnable {
         // 一个同步辅助类，它允许一组线程互相等待，直到到达某个公共屏障点 (common barrier point)
         private CyclicBarrier barrier;
         private String name;
         public Runner(CyclicBarrier barrier, String name) {
                   super();
                   this.barrier = barrier;
                   this.name = name;
         }
         @Override
         public void run() {
                   try {
                            Thread.sleep(1000 * (new Random()).nextInt(8));
                            System.out.println(name + " 准备好了...");
                            // barrier的await方法，在所有参与者都已经在此 barrier 上调用 await 方法之前，将一直等待
                            barrier.await();             // 最后一个线程的此函数执行完毕后将唤醒
                   } catch (InterruptedException e) {
                            e.printStackTrace();
                   } catch (BrokenBarrierException e) {
                            e.printStackTrace();
                   }
                   System.out.println(name + " 起跑！");
         }
}
```
## 交换器：
`Exchange`：运行两个线程在要交换的对象准备好时交换两个对象，当两个线程工作在同一数据结构的两个实例上的时候，一个向实例添加数据而另一个从实例清除数据  
## 同步对列：
`SynchronousQueue`：允许一个线程把对象交给另一个线程，在没有显示同步的情况下，当两个线程准备好将一个对象从一个线程传递到另一个时
一种将生产者和消费者配对的机制，当一个线程调用SynchronousQueue的put方法时，它会阻塞直到另一个线程调用take方法为止，反之亦然，与Exchange不同，数据仅沿着一个方向传递，从生产者到消费者；它不是一个队列，没有任何元素，size方法总是0  
