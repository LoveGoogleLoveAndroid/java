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
4. java.lang.reflect有三个类，Field、Method、Constructor
getFields、getMethods、getConstructors分别返回类提供的public域、方法和构造器，
其中包括超类的公有成员
getDeclareFields、getDeclareMethods、getDeclareConstructors分别返回类提供的public域、方法和构造器，其中包括私有和受保护的成员，但不包括超类的成员  
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
异常、日志、断言  
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
4. 参数化类型的数组不合法， Pair<String>[] table = new Pair<String>[10]; ERROR
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
