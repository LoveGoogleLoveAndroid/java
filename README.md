# java
java basic.


Java关键术语：
简单性（语法是C++的纯净版本，无头文件、指针、结构、联合、操作符重载、虚基类）、、面向对象、网络技能、健壮性、安全性、可移植性、解释性、高性能、多线程
源代码的文件名必须与公有类的名字相同
Java所有的方法必须是某个类的方法，包括main函数。
 
注释：
比C++多了文档注释/**   */
 
基本数据类型：
byte（1）、short（2）、int（4）、 long（8）、float（4）、double（8），char（1）、boolean（1），无无符号类型；整型值和布尔型不能相互转换
 
声明与定义：java中不做区分
 
字符串：
String greeting = “hello”;         // greeting更像是C++里面的指向常量的指针
greeting = greeting.substring(0, 3) + “p!”   // help!  
String为不可变字串，实际将greeting 指向另一个字符串，意味着堆中有两个字符串”hello”和”help!”；字符串+连接像是C++里面对String重载了+操作符
优点：编译器可以让字符串共享；Java设计者认为共享带来的高效率远胜提取，拼接字符串带来的低效率；可以用StringBuilder防止既耗时又费空间的链接操作
StringBuilder builder = new StringBuilder();
builder.append(ch);
builder.append(str);
String completedString = builder.toString();
 
int compareTo(String other);   // 按字典顺序比较字符串
boolean equals(Object other); // 比较两个对象的值
==  // 比较两个对象的地址
 
块作用域：
C++中可以在块中重定义同名变量，且会覆盖外层变量，Java中不允许这样做
 
循环：
Java中不支持goto，但是可以通过break加标签的形式跳出多层循环；不止循环，标签可用到任何语句中
Label:
{
         If (condition)
                   break Lable；
}
 
for( variable:collection ) statement;
collection必须是一个数据或者是实现了Iterable接口的类对象（如ArrayList）
 
 
类之间关系：
继承（is-a）、实现（implements）、聚合（has-a）、组合、依赖（uses-a）、关联
 
对象：
Java中的对象变量（或者叫对象引用）与C++中的引用不同，C++中没有空引用，而且引用不能被赋值，它更像是C++中的对象指针
Date birthday;  // java
等同于：
Data * birthday; // C++
 
构造器：
与类名相同、每个类可以有多个构造器、可以有任意类型和个数的参数，但是无返回值、在创建对象的时候由系统调用，不能手动调用
 
私有方法：
有时候一个计算代码有若干个辅助方法，这些辅助方法不应该成为共有接口的一部分；或者需要一个特别的调用次序，只有最先调用的接口可设计为公有接口
 
final实例域：
final大多应用于基本数据类型或不可变类对象（如果类中的每个方法都不会改变其对象，就是不可变的类）；对于可变类，用final修饰会误导读者
private final Date hireDate;  // 即C++的常指针，一旦初始化，无法指向其他对象
 
静态域：
静态变量使用不多，静态常量使用很多
public class Math
{
         public static final double PI=3.1415926;
}
public class System
{
         public static final PrintStream out = …;
}
 
静态方法：
无this指针，只可访问静态域
两种常用场景：一个方法无需访问对象状态或只需访问静态域
 
static的前世今生：
1：最早用作C里面标识局部变量的存储属性，对比auto
2：重用在C里面修饰全局变量和函数，修改其访问属性，对比extern
3：C++中表示不属于对象而属于整个类的变量和函数
4：Java中含义与C++完全相同
 
参数传递：
值传递；C++除了值传递，还有引用传递；Java中的对象引用类似于C++的对象指针传递
 
方法签名：
返回类型不是方法签名的一部分，即不能有两个同名，参数类型也相同却返回类型不同的方法
 
初始化顺序：
1：类中域系统会默认初始化，数值为0，布尔false，对象引用null，但是局部变量不会
2：按照声明次序执行类中域赋值语句（C++中不能直接初始化实例域，所有的域必须在构造器中初始化，但是有一个初始化列表的语法可以进行设置）和初始化块（静态初始化块早于普通初始化块）
3：如果构造器调用了第二个构造器，则执行第二个构造器
4：执行这个构造器
 
构造函数：
如果类中提供了至少一个构造器，但是没有提供默认的构造器（即无参构造器），则在创建对象时如果没有提供构造参数会被视为不合法（仅当类中没有提供任何构造器的时候，系统才会提高一个默认的构造器）
 
this指针：
1：做隐形参数（同C++）
2：用于调用另一个构造器（C++中不允许在一个构造器里调用另一个）
Public Employee(double s)
{
         this(“Employee #” + nextId, s);
         nextId++;
}
 
super关键字：
1：调用超类的方法
2：调用超类的构造器（C++则采用作用域标识符：：）
 
 
析构器：
Java不支持，但可以为任何类添加finalize方法，在垃圾回收清除对象之前调用，不能依赖他回收任何稀缺的资源，应该由人工管理
 
包：
从编译器的角度看，嵌套的包之间没有任何关系，如java.util和java.util.jar
如何没有制定任何访问修饰符，则默认为包作用域，可被包中所有方法访问
 
类的定义格式：
1：public部分 2：包作用域部分 3：private部分
每个部分定义顺序：
1：实例方法 2：静态方法 3：实例域 4：静态域
 
多重继承：
Java用extends关键字代替了C++的:；而且跟C++不同，Java中不支持多重继承，而且所有的继承都是public继承
 
动态绑定：
1：Java的默认处理方式，如果希望一个方法不具有虚拟特征，可标记为final；C++默认是静态绑定
2：返回类型并不是签名的一部分，在覆盖方法时，一定要保证返回类型的兼容性，子类覆盖方法的返回类型必须与父类一样，或者是其子类型，而且子类方法的可见性不能低于父类，如父类中为public，则子类也必须是public
3：静态绑定的方法：private方法、static方法、final方法和构造器，因为编译器可以准确的知道调用的是哪个方法
4：final类（其中的方法自动为final，但不包括域）可阻止继承，final方法可阻止覆盖
C++中没有阻止覆盖的方法，阻止继承的技巧：
 
强制类型转换：
1：唯一原因是在暂时忽略了对象的实际类型后可以使用对象的全部功能
2：将子类引用赋给父类引用可以，反之必须进行强制类型转换
3：只能在继承层次进行类型转换
4：将父类转换为子类前，应该使用instanceof进行类型检查
 
抽象类：
1：为了提高程序的清晰度，包含一个或多个抽象方法的类必须声明为抽象的，关键字abstract，C++中无专门的关键字
2：抽象类可以包括具体数据和方法
3：即使类中不含抽象方法，也可声明为抽象类
4：抽象类不能实例化，但是可以创建抽象类的对象变量
 
protected：
java中其作用域是派生类和整个包，而C++中只有派生类可访问
 
Object：
1：只有基本类型不是对象，所有的数组类型都扩展于Object类；C++没有根基，但是每个指针都可以转换为void *
Object obj = new int[10];
2：equals方法的标准写法
public boolean equals( Object otherobj )
{
        If ( this == otherObj )       return true;
         If ( otherObj == null )       return false;
         If ( getClass() != otherObj.getClass() )    return false;
         Employee other = (Employee)otherObj;
 
         return ( name.equals(other.name) && salary == otherObj.salary && hireDay.equals( OtherObj.hireDay );
 
}
3：hashCode方法必须与equals的定义一致，如果重新定义equals方法，则必须重新定义hashCode方法，每个对象默认的散列码是其存储地址
4：toString方法用于返回表示对象值的字符串，只要对象与一个字符串通过操作符+连接，就会自动调用该方法，以获取这个对象的字符串描述
 
对象包装器：
所有的基本类型都有一个与之对应的类，这些类称为包装器
Integer Long Float Double Short Byte Character Void Boolean（前六个派生于Number）,对象包装器是不可变的，还是final，因此不能定义它们的子类，尖括号内的不允许是基本类型
ArraryList<Integer> list = new ArrayList<Integer>();
ArrayList<Integer>的效率要远低于int[]数组，适合构造小型集合，程序猿操作的方便性要比执行效率更加重要
自动打包：
list.add(3)将自动变换为list.add(new Integer(3));
自动拆包：
int n = list.get(3)将自动变换为int n = list.get(3).intValue();
字符串转为整型：
int x = Integer.parseInt(s);
Integer y = Integer.valueOf(s);
整型转为字符串：
String s = Integer.
 
修改参数值的方法：使用IntHolder、BooleanHolder等
