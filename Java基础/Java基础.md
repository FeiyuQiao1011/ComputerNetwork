# Java基础

- java语言特点
  - 简单易学
  - 面向对象
  - 平台无关性（Java虚拟机）
  - 支持多线程，内置多线程机制
  - 可靠
  - 安全
  - 支持网络编程
  - 解释与编译并存

- JVM vs JDK vs JRE

  - JVM

    Java虚拟机

    ![运行在 Java 虚拟机之上的编程语言](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/java-virtual-machine-program-language-os.png)

  - JDK

    Java Development Kit，创建和编译Java程序的工具，**包含JRE**，还有编译源码的编译器javac，文档注释工具javadoc，调试器jdb，反编译工具javap等

  - JRE

    Java Runtime Environment，Java运行环境，**包括JVM和Java基础类库**

  ![JDK 包含 JRE](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/jdk-include-jre.png)

- 什么是字节码？采用字节码的好处是什么？

  - JVM可以理解的代码，**扩展名为.class的文件**

  - 好处

    - 一定程度上解决了传统解释性语言执行效率较低的问题，同时又保留了解释性语言可移植的特点
    - 一次编译，随处运行，**只面向JVM**

    ![Java程序转变为机器代码的过程](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/java-code-to-machine-code.png)

    - .class文件 -> 机器码

      - JVM首先加载字节码文件

      - 通过解释器逐行解释执行

      - JIT(just-in-time compilation)编译器,运行时编译，完成一次编译后保存字节码对应机器码，**热点代码**，

      - **That‘s why we said Java is a language which 解释与编译共存**

        ![Java程序转变为机器代码的过程](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/java-code-to-machine-code-with-jit.png)

- JVM模型

  ![JVM 的大致结构模型](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/jvm-rough-structure-model.jpeg)

- Why 解释与编译共存？

  - 编译型
    - 通过编译器将源代码一次性翻译成机器码。**执行速度快，开发效率低**
  - 解释型
    - 通过解释器逐行解释成机器码再执行，**开发效率高，执行速度慢**

  ![编译型语言和解释型语言](/Users/qiaofeiyu/Desktop/java/计算机网络/JAVAWEB.assets/compiled-and-interpreted-languages.png)

  - 为什么说Java共存？
    - 因为Java解释与编译共存，先编译成字节码，.class文件，字节码须由解释器执行

- Java vs C++
  - Java不提供指针，内存更安全
  - Java单继承，C++支持多重继承
  - Java有自动内存管理垃圾回收机制GC，不需要手动释放内存
  - Java只支持方法重载，C++还支持操作符重载

- Java基本数据类型

  - 数字类型

    - 4种整形

      byte, short, int, long

    - 2种浮点型

      float，double

  - 字符型

    char

  - 布尔型

    boolean

  - 对应包装类

    - Byte
    - Short
    - Integer
    - Long
    - Float
    - Double
    - Character
    - Boolean

- 基本类型 vs 包装类型

  - 用途

    基本类型用于定义常量，局部变量，**包装类可用于泛型**

  - 存储方式

    基本类型的局部变量放在JVM栈中的局部变量表中，基本数据类型的成员变量（未被static修饰）放在java虚拟机的堆中。**包装类型属于对象类型**，对象实例放在堆中。

  - 占用空间

    基本数据类型占用空间较小

  - 默认值

    成员变量包装类型不赋值默认为null，基本数据类型有默认值，不是null

  - 比较方式

    对于基本数据类型来说，==比较的是值

    对于包装类型来说，==比较的是内存地址，所有整形包装类的值比较用equals( )方法

- 包装类型的缓存机制
  - Byte，Short，Integer，Long默认创建[-128,127]的缓存数据
  - Character创建了[0，127]范围的缓存数据
  - Boolean直接返回true，false
  - **超出范围还是创建对象**
  - Float，Double没有创建缓存机制

- 装箱 & 拆箱

  - 装箱：将基本数据类型用他们对应的引用类型包装起来

  - 拆箱：把包装类型转换为基本的数据类型

    ```java
    Integer i = 10;//装箱
    int n = i;//拆箱
    ```

- 关于浮点数精度

  - 计算机是二进制的，计算机在表示一个数字时，是有宽度的。无限循环小数只能被截断，会导致小数精度发生丢失的情况。

  - 如何解决？

    - BigDecimal

      ```java
      BigDecimal a = new BigDecimal("1.0");
      BigDecimal b = new BigDecimal("0.9");
      BigDecimal c = new BigDecimal("0.8");
      
      BigDecimal x = a.subtract(b);
      BigDecimal y = b.subtract(c);
      
      System.out.println(x); /* 0.1 */
      System.out.println(y); /* 0.1 */
      System.out.println(Objects.equals(x, y)); /* true */
      ```

- 超过Long的整形怎么表示？

  - BigInteger内部使用int[]数组来存储任意大小的整形数据

- 成员变量 vs 局部变量

  - 语法形式

    - 成员变量属于类，局部变量是在代码块或方法中定义的参数
    - 成员变量可以被访问修饰符和static修饰，局部变量不行
    - 都可以被final修饰

  - 存储方式

    - 成员变量使用static修饰，属于类
    - 不被static修饰，属于实例，随对象存在于堆内存中
    - 局部变量在栈中

  - 生存时间

    - 成员变量是对象的一部分，随对象创建而存在
    - 局部变量随方法调用自动生成，随方法结束而消亡

  - 默认值

    - 成员变量没有被赋值，会以类型默认值，**final修饰的成员变量必须显式赋值**
    - 局部变量不会默认赋值

    ```java
    public class VariableExample {
    
        // 成员变量
        private String name;
        private int age;
    
        // 方法中的局部变量
        public void method() {
            int num1 = 10; // 栈中分配的局部变量
            String str = "Hello, world!"; // 栈中分配的局部变量
            System.out.println(num1);
            System.out.println(str);
        }
    
        // 带参数的方法中的局部变量
        public void method2(int num2) {
            int sum = num2 + 10; // 栈中分配的局部变量
            System.out.println(sum);
        }
    
        // 构造方法中的局部变量
        public VariableExample(String name, int age) {
            this.name = name; // 对成员变量进行赋值
            this.age = age; // 对成员变量进行赋值
            int num3 = 20; // 栈中分配的局部变量
            String str2 = "Hello, " + this.name + "!"; // 栈中分配的局部变量
            System.out.println(num3);
            System.out.println(str2);
        }
    }
    ```

- 静态变量

  - 被static修饰的变量

  - 被所有实例共享

  - 通过类名来访问，例如StaticVariableExample.staticVar。被private修饰除外

    ```java
    public class StaticVariableExample {
        // 静态变量
        public static int staticVar = 0;
    }
    ```

  - 一般情况下静态变量会被final修饰，成为常量

    ```java
    public class ConstantVariableExample {
        // 常量
        public static final int constantVar = 0;
    }
    ```

- 字符串常量 vs 字符型常量
  - 字符常量‘ ’，字符串常量“ ”
  - 字符常量相当于一个整形，可以参与运算，字符串常量代表一个地址，**指向该字符串在内存中的存放位置**
  - 字符常量占2字节，字符串常量占若干字节

- 静态方法为什么不能调用非静态成员
  - 静态方法属于类，随类加载，可以通过类名直接访问。
  - 非静态成员属于对象，只有在对象实例化后才存在，通过实例化的对象访问
  - 非静态成员不存在的时候静态方法就存在了，内存中还不存在非静态成员，非法操作

- 静态方法 vs 实例方法
  - 静态方法可以使用类名.方法名调用，也可以使用对象.方法名调用
  - 实例方法只能通过对象.方法名调用
  - 静态方法只允许访问静态成员，不允许访问实例成员，实例方法不存在这个限制

- 重写 vs 重载
  - 重写override
    - 程序运行期间，子类对父类方法的重新编写
      - 方法名，参数列表必须相同，子类方法返回值小于等于父类方法，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类
      - 如果父类方法是private/final/static，子类不能重写,被static修饰的方法能够被再次声明
      - 构造方法无法被重写
    - 对于重写的返回值类型，如果方法的返回值类型是void和基本数据类型，返回值重写时不可修改。但是如果方法的返回值是引用类型，重写时是可以返回该引用类的子类的。
  - 重载
    - 发生在同一个类中，或者子类和父类之间，方法名必须相同，参数类型不同，个数不同，顺序不同，方法返回值和访问修饰符可以不同
    - **重载就是一个类中或者子父类中多个同名方法根据传入参数的不同执行不同的处理逻辑**

- 什么是可变长参数？

  - 允许在调用方法时传入不定长度的参数

    ```java
    public static void method1(String... args){
      
    }
    ```

  - 可变长参数只能作为函数的最后一个参数，但是前面也可以有其他类型的参数

    ```java
    public static void method2(String arg1, String... args){
      
    }
    ```

    **遇到方法重载时，优先匹配固定参数的方法，匹配度更高**

    **可变参数编译后实际会被转换成一个数组**

- 面向对象和面向过程的区别？
  - 面向过程把解决问题的过程拆成一个个方法，通过一个个方法解决问题
  - 面向对象会先抽象出对象，然后用对象执行方法的方式解决问题
  - 面向对象开发更易维护、复用、扩展

- 对象实体和对象引用？
  - 对象引用指向对象实例，对象引用存放在栈内存中
  - 1个对象引用可以指向0个或1个对象
  - 一个对象可以有n个引用指向他

- 对象的相等和引用相等的区别
  - 对象的相等一般比较的是内存中存放的内容是否相等
  - 引用相等一般比较的是他们指向的内存地址是否相等

- 一个类如果没有声明构造方法，可以执行吗？
  - 构造方法是一种特殊的方法，用于完成对象的初始化操作
  - 如果没有声明构造方法，会执行默认的无参构造方法
  - 如果有显示的带参数的构造方法，就先执行带参数的

- 构造方法有哪些特点？是否可以被override？
  - 名字与类相同
  - 没有返回值，但是不用void
  - 生成类的对象时自动执行，无需调用
  - 可以被重载

- 面向对象三大特征
  - 封装
    - 把一个对象的信息状态隐藏在对象内部，不允许直接访问。
    - 提供一个方法用来访问
  - 继承
    - 不同类型的对象，有一定数量的共同点
    - 子类对象拥有父类对象的所有属性和方法，**父类私有属性子类无法访问**
    - 子类可以拥有自己的属性和方法，**即子类可扩展**
    - 子类可以用自己的方式实现父类方法
  - 多态
    - 一个对象具有多种状态，父类的引用指向子类的实例
    - 对象类型和引用类型之间具有继承（类）/实现（接口）的关系
    - 多态不能调用只在子类但是不在父类的方法
    - 子类重写父类，真正执行的是子类覆盖的方法，否则，执行父类的方法

- 接口和抽象类
  - 都不能实例化
  - 都可以包含抽象方法
  - 都可以有默认的实现方法
  - 接口主要用于对类的行为约束，抽象类主要用于代码复用，强调的是所属关系
  - 一个类只能继承一个类，但是可以实现多个接口
  - 接口中的成员变量必须是public static final类型的，不能被修改且必须有初始值，抽象类的成员变量默认default，可在子类中被重新定义，也可以被重新赋值

- 深拷贝和浅拷贝

  - 浅拷贝

    在堆上创建一个新的对象（区别于引用拷贝），不过，如果原对象内部的属性是引用类型的话，浅拷贝会直接复制对象的引用地址，**拷贝对象与原对象共用一个内部对象**

    ```java
    //浅拷贝
    public class Address implements Cloneable{
        private String name;
        // 省略构造函数、Getter&Setter方法
        @Override
        public Address clone() {
            try {
                return (Address) super.clone();
            } catch (CloneNotSupportedException e) {
                throw new AssertionError();
            }
        }
    }
    
    public class Person implements Cloneable {
        private Address address;
        // 省略构造函数、Getter&Setter方法
        @Override
        public Person clone() {
            try {
                Person person = (Person) super.clone();
                return person;
            } catch (CloneNotSupportedException e) {
                throw new AssertionError();
            }
        }
    }
    ```

    

  - 深拷贝

    完全复制这个对象

    ```java
    //深拷贝
    @Override
    public Person clone() {
        try {
            Person person = (Person) super.clone();
            person.setAddress(person.getAddress().clone());
            return person;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
    
    Person person1 = new Person(new Address("武汉"));
    Person person1Copy = person1.clone();
    // false
    System.out.println(person1.getAddress() == person1Copy.getAddress());
    ```

    ![浅拷贝、深拷贝、引用拷贝示意图](../java/计算机网络/JAVAWEB.assets/shallow&deep-copy.png)

- Object

  ```java
  /**
   * native 方法，用于返回当前运行时对象的 Class 对象，使用了 final 关键字修饰，故不允许子类重写。
   */
  public final native Class<?> getClass()
  /**
   * native 方法，用于返回对象的哈希码，主要使用在哈希表中，比如 JDK 中的HashMap。
   */
  public native int hashCode()
  /**
   * 用于比较 2 个对象的内存地址是否相等，String 类对该方法进行了重写以用于比较字符串的值是否相等。
   */
  public boolean equals(Object obj)
  /**
   * naitive 方法，用于创建并返回当前对象的一份拷贝。
   */
  protected native Object clone() throws CloneNotSupportedException
  /**
   * 返回类的名字实例的哈希码的 16 进制的字符串。建议 Object 所有的子类都重写这个方法。
   */
  public String toString()
  /**
   * native 方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
   */
  public final native void notify()
  /**
   * native 方法，并且不能重写。跟 notify 一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
   */
  public final native void notifyAll()
  /**
   * native方法，并且不能重写。暂停线程的执行。注意：sleep 方法没有释放锁，而 wait 方法释放了锁 ，timeout 是等待时间。
   */
  public final native void wait(long timeout) throws InterruptedException
  /**
   * 多了 nanos 参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 毫秒。。
   */
  public final void wait(long timeout, int nanos) throws InterruptedException
  /**
   * 跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
   */
  public final void wait() throws InterruptedException
  /**
   * 实例被垃圾回收器回收的时候触发的操作
   */
  protected void finalize() throws Throwable { }
  ```

- ==和equals()的区别

  - ==
    - 对于基本数据类型，比较的是值
    - 对于引用类型，比较的是地址
  - equals（）
    - 不能判断基本数据类型的变量，只能判断两个对象是否相等
    - equals方法存在于Object类中，而Object是所有类的父类，**所有类都有equals方法**
    - equals没有被重写，相当于==
    - 重写，可以比较对象中属性

  **String重写了equals方法**

  ```java
  public boolean equals(Object anObject) {
      if (this == anObject) {
          return true;
      }
      if (anObject instanceof String) {
          String anotherString = (String)anObject;
          int n = value.length;
          if (n == anotherString.value.length) {
              char v1[] = value;
              char v2[] = anotherString.value;
              int i = 0;
              while (n-- != 0) {
                  if (v1[i] != v2[i])
                      return false;
                  i++;
              }
              return true;
          }
      }
      return false;
  }
  ```

- hashCode( )有什么用？
  - hashCode（）定义在JDK的Object类中，任何Java类都包含hashCode（）函数。Object的hashCode（）方法是本地方法，使用C语言、C++实现的

- 为什么要有hashCode？
  - 当把对象加入HashSet时，HashSet会计算对象的hashCode值来判断对象加入的位置，同时也会跟已经加入的对象的hashCode值做比较，如果没有hashCode相同，HashSet就可以认为对象没有重复出现.如果hashCode值相同，会调用equals方法来检查hashCode相等的对象是否真的相同，若二者相同，HashSet就不会让其加入成功。若不同，就会重新散列到其他位置。**大大减少了equals的调用次数，提高执行速度**
  - hashCode（）和equals（）都是用于比较两个对象是否相等
    - 在一些容器中，类似hashMap、hashSet，hashCode判断效率高
    - hashCode缩小查找成本
    - **两个对象的hashCode值相等并不代表两个对象就相等**
  - 如果两个对象的`hashCode` 值相等，那这两个对象不一定相等（哈希碰撞）。
  - 如果两个对象的`hashCode` 值相等并且`equals()`方法也返回 `true`，我们才认为这两个对象相等。
  - 如果两个对象的`hashCode` 值不相等，我们就可以直接认为这两个对象不相等。

- 为什么重写equals方法一定重写hashCode方法？
  - 两个相等对象的hashCode必然相等。如果equals方法判断两个对象相等，那么hashCode的值也要相等
  - 如果重写equals方法但是不重写hashCode方法，那么equals方法判断相等的两个对象，hashCode可能不同

- String、StringBuffer、StringBuilder的区别？

  - String不可变

  - StringBuffer 和 StringBuilder都继承自AbstractStringBuilder类

  - **底层使用字符数组保存字符串**

    ```java
    abstract class AbstractStringBuilder implements Appendable, CharSequence {
        char[] value;
        public AbstractStringBuilder append(String str) {
            if (str == null)
                return appendNull();
            int len = str.length();
            ensureCapacityInternal(count + len);
            str.getChars(0, len, value, count);
            count += len;
            return this;
        }
      	//...
    }
    ```

  - 线程安全性
    - String对象不可变，可以认为是常量，线程安全
    - StringBuffer对方法加了同步锁或对调用的方法加了同步锁，线程安全
    - StringBuilder并没有对方法加同步锁，非线程安全
  - 性能
    - 对String改变时，会生成新的String对象，指针指向新的String对象
    - StringBuffer每次都会对StringBuffer对象本身进行操作，而不生成新的对象并改变对象引用
    - StringBuilder更好一点，但是线程不安全
  - 操作少量的数据，String
  - 单线程操作字符串缓冲区下操作大量数据，StringBuilder
  - 多线程，StringBuffer

- String为什么不可变？

  - 保存字符串的数组被final修饰且为私有，String类并没有提供修改这个字符串的方法

    ```java
    public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
        private final char value[];
    	//...
    }
    ```

  - String类被final修饰导致其不能被继承，避免子类破坏String

  - **Java9之后，String的实现该用byte数组**

    ```java
    public final class String implements java.io.Serializable,Comparable<String>, CharSequence {
        // @Stable 注解表示变量最多被修改一次，称为“稳定的”。
        @Stable
        private final byte[] value;
    }
    
    abstract class AbstractStringBuilder implements Appendable, CharSequence {
        byte[] value;
    
    }
    ```

- 关于字符串拼接 “+” “+=” StringBuilder

  - +和+=是唯二的两个重载过的运算符

  - +拼接字符串实际是通过StringBuilder调用append()方法实现的，拼接完之后调用toString()得到一个String对象

    ```java
    String str1 = "he";
    String str2 = "llo";
    String str3 = "world";
    String str4 = str1 + str2 + str3;
    ```

    ![img](../java/计算机网络/JAVAWEB.assets/image-20220422161637929.png)

  - 再循环内调用+，会有明显缺陷，编译器会创建多个StringBuilder对象

    ```java
    String[] arr = {"he", "llo", "world"};
    String s = "";
    for (int i = 0; i < arr.length; i++) {
        s += arr[i];
    }
    System.out.println(s);
    ```

    ![img](../java/计算机网络/JAVAWEB.assets/image-20220422161320823.png)

    - **在循环外创建StringBuilder对象**

      ```java
      String[] arr = {"he", "llo", "world"};
      StringBuilder s = new StringBuilder();
      for (String value : arr) {
          s.append(value);
      }
      System.out.println(s);
      ```

      ![img](../java/计算机网络/JAVAWEB.assets/image-20220422162327415.png)

- String的equals()方法和Object的equals()方法有什么区别？

  - String的equals方法是被重写过的，比较的是String字符串的值是否相等
  - Object的equals方法比较的是对象的地址

- 字符串的常量池

  - JVM为了提升性能和减少内存的消耗，为字符串String类专门开辟的区域，主要目的是为了避免字符串的重复创建

  - ```java
    // 在堆中创建字符串对象”ab“
    // 将字符串对象”ab“的引用保存在字符串常量池中
    String aa = "ab";
    // 直接返回字符串常量池中字符串对象”ab“的引用
    String bb = "ab";
    System.out.println(aa==bb);// true
    ```

- String s1 = new String("abc")这句话创建了几个字符串对象？

  - 会创建1个或2个字符串对象

  - 字符串常量池不存在字符串对象“abc”的引用

    ![img](../java/计算机网络/JAVAWEB.assets/image-20220413175809959.png)

  - 字符串常量池中存在字符串对象“abc”的引用

    - 在堆中创建一个字符串对象“abc”

- String.intern()方法

  - 本地方法（native），作用是将指定的字符串对象的引用保存在字符串常量池中

    - 如果字符串常量池保存了对应的字符串对象的引用，那就直接返回引用

    - 如果没保存，则在常量池中创建一个指向该字符的对象的引用并返回

      ```java
      // 在堆中创建字符串对象”Java“
      // 将字符串对象”Java“的引用保存在字符串常量池中
      String s1 = "Java";
      // 直接返回字符串常量池中字符串对象”Java“对应的引用
      String s2 = s1.intern();
      // 会在堆中在单独创建一个字符串对象
      String s3 = new String("Java");
      // 直接返回字符串常量池中字符串对象”Java“对应的引用
      String s4 = s3.intern();
      // s1 和 s2 指向的是堆中的同一个对象
      System.out.println(s1 == s2); // true
      // s3 和 s4 指向的是堆中不同的对象
      System.out.println(s3 == s4); // false
      // s1 和 s4 指向的是堆中的同一个对象
      System.out.println(s1 == s4); //true
      ```


- String类型的变量和常量做“+”运算时发生了什么？

  不加final的情况

  ```java
  //Object的equals方法比较的是对象的内存地址
  //String的equals方法比较的是字符串的值是否相等
  String str1 = "str";
  String str2 = "ing";
  String str3 = "str" + "ing";
  String str4 = str1 + str2;
  String str5 = "string";
  System.out.println(str3 == str4);//false
  System.out.println(str3 == str5);//true
  System.out.println(str4 == str5);//false
  ```

  - 对于编译器可以确定值的字符串，也就是常量字符串，JVM会将其存入字符串常量池。并且，字符串拼接得到的字符串常量在编译阶段就已经被放到字符串常量池
  - 引用的值在编译阶段是无法确定的，编译器无法对其优化

  - 对象引用“+”的字符串的拼接方式，实际上是通过StringBuilder调用append（）方法实现的，拼接完成后调用toSrting（）得到一个String对象

    ```java
    String str4 = new StringBuilder().append(str1).append(str2).toString();
    ```

- 异常

  ![Java 异常类层次结构图](../java/计算机网络/JAVAWEB.assets/types-of-exceptions-in-java.png)

- Exception和Error有什么区别？
  - Exception 程序本身可以处理的异常，可以通过catch捕获
    - Checked Exception，受检查异常，必须处理
    - Unchecked Exception，不受检查异常，可以不处理
  - Error 程序无法处理的异常

- Checked Exception vs Unchecked Exception
  - Checked Exception没有被catch或throw关键字处理的话，没办法通过编译
    - RuntimeException
      - NullPointerException
      - IllegalArguementException 传参错误
      - NumberFormatException 字符串转换为数字格式错误
      - ArrayIndexOutOfBoundException 数组越界错误
      - ClassCastException 类型转换错误
      - ArithmeticException 算数错误
  - Unchecked Exception
    - 在编译过程中不处理也可以通过编译

- Throwable类常用方法有哪些？

  ```java
  String getMessage();//返回异常发生时的简要描述
  String toString();//返回异常发生时的详细信息
  String getLocallizedMessage();//返回异常发生时的本地化信息
  ```

- Try-catch-finally

  - try用于捕获异常，其后可接0个或多个catch块，如果没有catch则必须跟finally

  - catch，用于处理try捕获到的异常

  - finally，无论是否捕获或处理异常，finally语句块的内容都会被执行。**当try或者catch方法中有return，return前先执行finally**

  - **不可以在finally中用return**

    - 如果try和finally中都有return，try中的return会被忽略

      ```Java
      public static void main(String[] args) {
          System.out.println(f(2));
      }
      
      public static int f(int value) {
          try {
              return value * value;
          } finally {
              if (value == 2) {
                  return 0;
              }
          }
      }//输出0
      ```

- finally中的方法一定会被执行吗？

  - 不一定

    - 在finally之前关闭虚拟机

      ```java
      try {
          System.out.println("Try to do something");
          throw new RuntimeException("RuntimeException");
      } catch (Exception e) {
          System.out.println("Catch Exception -> " + e.getMessage());
          // 终止当前正在运行的Java虚拟机
          System.exit(1);
      } finally {
          System.out.println("Finally");
      }
      ```

    - 程序所在的线程死亡

    - 关闭CPU

  - 使用try-with-resources代替try-catch-finally

    ```java
    //读取文本文件的内容
    Scanner scanner = null;
    try {
        scanner = new Scanner(new File("D://read.txt"));
        while (scanner.hasNext()) {
            System.out.println(scanner.nextLine());
        }
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } finally {
        if (scanner != null) {
            scanner.close();
        }
    }
    ```

    ```java
    //try-with-resources改造
    try (Scanner scanner = new Scanner(new File("test.txt"))) {
        while (scanner.hasNext()) {
            System.out.println(scanner.nextLine());
        }
    } catch (FileNotFoundException fnfe) {
        fnfe.printStackTrace();
    }
    ```

- 泛型

  - 编译器可以对泛型参数进行检测，并且通过泛型参数可以指定传入参数的对象类型

    ```java
    ArrayList<Person> persons = new ArrayList<person>(); 
    ```

- 泛型使用方式

  - 泛型类

    ```java
    //此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
    //在实例化泛型类时，必须指定T的具体类型
    public class Generic<T>{
    
        private T key;
    
        public Generic(T key) {
            this.key = key;
        }
    
        public T getKey(){
            return key;
        }
    }
    
    //实例化泛型
    Generic<Integer> genericInteger = new Generic<Integer>(123456);
    ```

  - 泛型接口

    ```java
    public interface Generator<T> {
        public T method();
    }
    
    //实现泛型接口，不指定类型
    class GeneratorImpl<T> implements Generator<T>{
        @Override
        public T method() {
            return null;
        }
    }
    
    //实现泛型接口，指定类型
    class GeneratorImpl<T> implements Generator<String>{
        @Override
        public String method() {
            return "hello";
        }
    }
    ```

  - 泛型方法

    ```java
       public static < E > void printArray( E[] inputArray )
       {
             for ( E element : inputArray ){
                System.out.printf( "%s ", element );
             }
             System.out.println();
        }
    
    //使用
    // 创建不同类型数组：Integer, Double 和 Character
    Integer[] intArray = { 1, 2, 3 };
    String[] stringArray = { "Hello", "World" };
    printArray( intArray  );
    printArray( stringArray  );
    ```

- 反射

  - 框架灵魂。运行时分析类以及执行类中方法的能力。通过反射可以获得任意一个类的所有方法和属性，也可以调用这些方法和属性。

- 反射应用场景

- 注解

  - 特殊的注释，主要用于修饰类、方法或者变量，提供某些信息供程序在编译或运行时使用

    ```java
    @Target(ElementType.METHOD)
    @Retention(RetentionPolicy.SOURCE)
    public @interface Override {
    
    }
    
    public interface Override extends Annotation{
    
    }
    ```

  - 注解的解析方法

    - 编译期直接扫描
    - 运行期通过反射处理

- SPI

  - Service Provider Interface

  - vs API

    ![img](../java/计算机网络/JAVAWEB.assets/1ebd1df862c34880bc26b9d494535b3dtplv-k3u1fbpfcp-watermark.png)

- 序列化和反序列化

  - 持久化Java对象比如将Java对象保存在文件中，在网络中传输Java对象

  - 序列化：将数据结构或者对象转化成二进制字节流的过程

  - 反序列化：将在序列化过程中所生成的二进制字节流转化成数据结构或者对象的过程

  - 场景：

    - 对象在进行网络传输，比如远程方法调用RPC的时候，之前需要先被序列化，接收方进行反序列化

    - 将对象存储到文件之前需要进行序列化，将对象从文件读取出来需要反序列化

    - 将对象存储到数据库（Redis）之前需要序列化，将对象从缓存数据中读取出来需要反序列化

    - 将对象存储到内存，需要序列化，从内存中读取之后反序列化。

      ![img](../java/计算机网络/JAVAWEB.assets/a478c74d-2c48-40ae-9374-87aacf05188c.png)

- Java值传递


  - 形参&实参


    - 形参：用于定义函数方法，接收实参，不需要有确定的值
    
    - 实参：用于传递函数方法的参数，必须有确定的值
    
      ```java
      String hello = "Hello!";
      // hello 为实参
      sayHello(hello);
      // str 为形参
      void sayHello(String str) {
          System.out.println(str);
      }
      ```

  - 值传递&引用传递


    - 值传递：方法接受的是实参值的拷贝，会创建副本
    - 引用传递：方法所接收的是实参所引用对象在堆中的地址，不会创建副本，对形参的修改将影响实参


- 为什么Java只有值传递？

  ```java
  public static void main(String[] args) {
      int num1 = 10;
      int num2 = 20;
      swap(num1, num2);
      System.out.println("num1 = " + num1);
      System.out.println("num2 = " + num2);
  }
  
  public static void swap(int a, int b) {
      int temp = a;
      a = b;
      b = temp;
      System.out.println("a = " + a);
      System.out.println("b = " + b);
  }
  
  /**
  a = 20
  b = 10
  num1 = 10
  num2 = 20
  **/
  
  //在swap方法中，a、b的值进行交换，并不会影响到num1、num2.因为a、b的值只是从num1、num2复制过去的
  //a、b相当于num1、num2的副本
  ```

  ![img](../java/计算机网络/JAVAWEB.assets/java-value-passing-01.png)

- 传递引用类型

  ```java
  	public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5 };
        System.out.println(arr[0]);
        change(arr);
        System.out.println(arr[0]);
  	}
  
  	public static void change(int[] array) {
        // 将数组的第一个元素变为0
        array[0] = 0;
  	}
  
  //输出
  1
  0
  ```

  ![img](../java/计算机网络/JAVAWEB.assets/java-value-passing-02.png)

  **change方法拷贝的是arr的地址，他和arr指向同一个数组对象**

- ```java
  public class Person {
      private String name;
     // 省略构造函数、Getter&Setter方法
  }
  
  public static void main(String[] args) {
      Person xiaoZhang = new Person("小张");
      Person xiaoLi = new Person("小李");
      swap(xiaoZhang, xiaoLi);
      System.out.println("xiaoZhang:" + xiaoZhang.getName());
      System.out.println("xiaoLi:" + xiaoLi.getName());
  }
  
  public static void swap(Person person1, Person person2) {
      Person temp = person1;
      person1 = person2;
      person2 = temp;
      System.out.println("person1:" + person1.getName());
      System.out.println("person2:" + person2.getName());
  }
  
  //输出
  person1:小李
  person2:小张
  xiaoZhang:小张
  xiaoLi:小李
  ```

  **swap方法的参数person1和person2只是拷贝的实参xiaozhang和xiaoli的地址，不影响实参本身**

  ![img](../java/计算机网络/JAVAWEB.assets/java-value-passing-03.png)

- 引用传递是怎样的？

```c++
#include <iostream>

void incr(int& num)
{
    std::cout << "incr before: " << num << "\n";
    num++;
    std::cout << "incr after: " << num << "\n";
}

int main()
{
    int age = 10;
    std::cout << "invoke before: " << age << "\n";
    incr(age);
    std::cout << "invoke after: " << age << "\n";
}

//输出
```

```text
invoke before: 10
incr before: 10
incr after: 11
invoke after: 11
```

**对形参的修改会影响实参的值。这里是因为incr形参的数据类型用的是int&才为引用传递，如果用int还是值传递**

- 总结
  - Java中将实参传递给方法或函数的方式是值传递
  - 如果参数是基本数据类型的话，传递的就是基本类型的字面量值的拷贝，会创建副本
  - 如果参数是引用类型，传递的就是实参所引起的对象在堆中地址值的拷贝，同样会创建副本。

- Java序列化

  - 什么是序列化？

    - 将数据结构或对象转换成二进制字节流的过程
    - 反序列化：将在序列化过程中生成的二进制字节流转换成数据结构或对象的过程

  - 常见应用场景

    - 对象在进行网络传输，比如远程方法调用RPC之前需要被序列化，接收到序列化的对象之后需要再进行反序列化

    - 将对象存储到文件之前需要序列化，将对象从文件中读取出来需要反序列化

    - 将对象存储到数据库中之前（Redis）需要序列化，将对象从缓存数据库读取出来需要反序列化

    - 将对象存储到内存之前需要序列化，从内存中读取出来之后需要进行反序列化

      ![img](../java/计算机网络/JAVAWEB.assets/a478c74d-2c48-40ae-9374-87aacf05188c-20230531085627923.png)

- 序列化协议属于TCP/IP的哪一层？

  ![TCP/IP 四层模型](../java/计算机网络/JAVAWEB.assets/tcp-ip-4-model.png)

​	表示层做的事情就是对应用层的用户数据进行处理，转换为二进制流，或者将二进制流转换为应用层的用户数据

​	OSI七层模型中应用层、表示层、会话层都属于TCP/IP四层模型中的应用层，所以序列化协议属于TCP/IP协议应用层的一部分

- 常见的序列化协议

  - JDK自带，实现java.io.Serializable接口

    ```java
    @AllArgsConstructor
    @NoArgsConstructor
    @Getter
    @Builder
    @ToString
    public class RpcRequest implements Serializable {
        private static final long serialVersionUID = 1905122041950251207L;
        private String requestId;
        private String interfaceName;
        private String methodName;
        private Object[] parameters;
        private Class<?>[] paramTypes;
        private RpcMessageTypeEnum rpcMessageTypeEnum;
    }
    ```

- serialVersionUID有什么作用？

  - 序列化号serialVersionUID属于版本控制的作用。反序列化时，会检查serialVersionUID是否和当前类的serialVersionUID一致。如果不一致则会抛出InvaildClassException异常

- serialVersionUID不是被static变量修饰了吗，为什么还会被序列化

  - static修饰的变量属于静态变量，位于方法区，不会被序列化。反序列化之后，static变量的值就像是默认赋予给了对象一样，看着就像被序列化了，其实没有

- 如果不想被序列化咋办？
  - 用transient关键字修饰
  - 阻止实例中那些用此关键字修饰的变量序列化，当对象被反序列化时，被transient修饰的变量值不会被持久化和恢复
  - 只能修饰变量，不能修饰方法和类
  - transient修饰的变量，在反序列化后变量值会被置成类型的默认值
  - static不属于任何对象，无论有没有transient关键字，都不会被序列化

- 反射机制

  - 什么是反射？

    - 运行时分析类以及执行类中方法的能力
    - 通过反射可以获取一个类的所有属性和方法，还可以调用这些属性和方法

  - 反射应用场景

    - 动态代理

      ```java
      public class DebugInvocationHandler implements InvocationHandler {
          /**
           * 代理类中的真实对象
           */
          private final Object target;
      
          public DebugInvocationHandler(Object target) {
              this.target = target;
          }
      
      
          public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
              System.out.println("before method " + method.getName());
              Object result = method.invoke(target, args);
              System.out.println("after method " + method.getName());
              return result;
          }
      }
      ```

    - 注解

- 反射机制优缺点
  - 代码更灵活
  - 安全问题

- 反射

  - 获取Class对象的四种方式

    - 知道具体类

      ```java
      Class alunbarClass = TargetObject.class;
      ```

    - 通过Class.forName()传入类的全路径获取

      ```java
      Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
      ```

    - 通过对象实例instance.getClass()获取

      ```java
      TargetObject o = new TargetObject();
      Class alunbarClass2 = o.getClass();
      ```

    - 通过类加载器xxxClassLoader.loadClass()传入类路径

      ```
      ClassLoader.getSystemClassLoader().loadClass("cn.javaguide.TargetObject");
      ```


  ## 集合概述

  Java集合，也叫做容器，主要由两大接口派生而来：一个是Collection接口，主要用于存放单一元素；另一个是Map接口，主要用于存放键值对。对于Collection接口，下面又有三个子接口：List、Set、Queue。

  ![Java 集合框架概览](../java/计算机网络/JAVAWEB.assets/java-collection-hierarchy.png)

- List,set,queue,map四者的区别
  - List：存储的元素是有序的、可重复的
  - Set：存储的元素是无序的，不可重复的
  - queue：按特定的排队规则来确定先后顺序。存储的元素是有序的、可重复的
  - Map：使用键值对存储，key是无序的，不可重复的，value是无序的，可重复的。

- Collection
  - List
    - ArrayList：Object[ ]数组
    - Vector: Object[ ]数组
    - LinkedList: 双向链表
  - Set
    - HashSet：无序，底层采用HashMap实现，保存元素
    - LinkedHashSet：LinkedHashSet是HashSet的子类，并通过LinkedHashMap来实现的
    - TreeSet：红黑树（自平衡的排序二叉树）
  - Queue
    - PriorityQueue: Object[ ]数组来实现二叉堆
    - ArrayQueue：Object[ ]数组 + 双指针

- Map

  - HashMap

    JDK1.8之前HashMap由数组+链表组成，数组是HashMap的主体，链表则是为了解决哈希冲突而存在的。JDK1.8以后在解决哈希冲突的时候有了较大变化，当链表长度大于阈值时（默认为8）（将链表转化成红黑树之前会判断，如果当前数组长度小于64，那么会选择先进行数组扩容，而不是转化成红黑树），将链表转化成红黑树，减少搜索时间

  - LinkedHashMap

    LinkedHashMap继承自HashMap，所以他的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，LinkedHashMap在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表的相应操作，实现了访问顺序的相关逻辑。

  - Hashtable

    数组+链表组成，数组是Hashtable的主体，链表则是为了解决哈希冲突而存在的

  - TreeMap

    红黑树

- 如何选用集合
  - 需要根据键值获取元素值时就选用Map接口下的集合，需要排序是时选择TreeMap，不需要排序时选择HashMap，保证线程安全就选用ConcurrentHashMap
  - 只需要存放元素值时，选择实现Collection接口的集合，需要保证元素唯一时实现set接口的集合比如TreeSet或HashSet，不需要就选择实现List接口的如ArrayList或LinkedList

- 为什么要使用集合

  当我们在存储同一种类型的一组数据时，数组就行。但是，在实际开发中，数组有缺点，存储的数据类型多种多样且不确定，这是java集合起作用。java集合提供了更灵活，更有效的方法来存储多个数据对象。Java集合框架中的各种集合类和接口可以存储不同类型和数量的对象，同时还具有多样化的操作方式。相较于数组，Java集合的优势在于大小可变、支持泛型、具有内建算法等。Java集合提高了数据存储和处理的灵活性。

- List

  - ArrayList和Array的区别

    **ArrayList基于动态数组实现，比Array使用起来更加灵活：**

    - ArrayList可以动态扩容或者缩容，而Array被创建之后就不可以改变长度了

    - ArrayList允许使用泛型来确保类型安全，Array不可以

    - ArrayList只能存储对象，对于基本数据类型，需要使用包装类，Array都可以直接存

    - ArrayList支持插入、删除、遍历等常见操作，并提供了丰富API；Array只是固定长度，只能按下标访问，不能动态增删

    - ArrayList创建时不需要指定大小，而Array创建时必须指定

      **Array**

      ```java
       // 初始化一个 String 类型的数组
       String[] stringArr = new String[]{"hello", "world", "!"};
       // 修改数组元素的值
       stringArr[0] = "goodbye";
       System.out.println(Arrays.toString(stringArr));// [goodbye, world, !]
       // 删除数组中的元素，需要手动移动后面的元素
       for (int i = 0; i < stringArr.length - 1; i++) {
           stringArr[i] = stringArr[i + 1];
       }
       stringArr[stringArr.length - 1] = null;
       System.out.println(Arrays.toString(stringArr));// [world, !, null]
      ```

      **ArrayList**

      ```java
      // 初始化一个 String 类型的 ArrayList
       ArrayList<String> stringList = new ArrayList<>(Arrays.asList("hello", "world", "!"));
      // 添加元素到 ArrayList 中
       stringList.add("goodbye");
       System.out.println(stringList);// [hello, world, !, goodbye]
       // 修改 ArrayList 中的元素
       stringList.set(0, "hi");
       System.out.println(stringList);// [hi, world, !, goodbye]
       // 删除 ArrayList 中的元素
       stringList.remove(0);
       System.out.println(stringList); // [world, !, goodbye]
      ```

- ArrayList可以添加null值吗？

  可以，可以添加任何值，但是不建议添加null，无意义难维护，如果忘记判空处理会导致空指针异常。

- ArrayList插入和删除元素的时间复杂度

  - 对于插入
    - 头部插入：所有元素向后移动一个位置，时间复杂度时O（n）
    - 尾部插入：当数组容量未达到极限时，往列表末尾插入元素的时间复杂度是O(1), 因为只需要在元素末尾添加一个元素即可；当容量达到极限需要扩容时，需要执行一次O（n）的操作将原数组复制到更大的数组，然后再执行O(1)操作插入数据
    - 指定位置插入：需要将指定位置之后的元素都向后移动一个位置，然后把新元素放入指定位置。这个过程需移动平均n/2个元素，时间复杂度为O（n）

  - 对于删除
    - 头部删除：所有元素向前移动一个位置，时间复杂度是O（n）
    - 尾部删除：O（1）
    - 指定位置删除：O（n）

- LinkedList插入和删除元素的时间复杂度
  - 头部插入/删除：只需要修改头节点的指针，时间复杂度是O（1）
  - 尾部插入/删除：只需要修改尾节点的指针，O（1）
  - 指定位置插入/删除：先移动到指定位置，再修改指定节点完成插入/删除，因此需要移动平均n/2个元素，时间复杂度为O（n）

- LinkedList为什么不能实现RandomAccess接口？

  RandomAccess是一个标记接口，用来表明实现该接口的类支持随机访问（可通过索引快速访问元素）。由于LinkedList底层数据结构是链表，内存地址不连续，只能通过指针来定位，不支持随机快速访问，所以不能实现RandomAccess接口。

- ArrayList与LinkedList区别
  - 是否线程安全：ArrayList和LinkedList都是不同步的，也就是不保证线程安全
  
  - 底层数据结构：ArrayList底层使用的是Object数组；LinkedList底层使用的是双向链表
  
  - 插入和删除是否受到元素位置影响
  
    - ArrayList采用数组存储，插入和删除元素的时间复杂度受元素位置的影响。
    - LinkedList采用链表存储，在头尾插入不受元素位置的影响。指定位置插入，需要先移动到指定位置，O（N）复杂度。
  
  - 是否支持快速随机访问
  
    LinkedList不支持高效的随机访问，ArrayList实现了RandomAccess接口。支持快速随机访问。
  
  - 内存空间占用
  
    ArrayList空间浪费主要体现在list列表的结尾会预留一定空间，而LinkedList的空间花费则体现在他的每个元素都要消耗比ArrayList更多的空间（存放后继、前驱、数据）

- 双向链表和双向循环链表

  - 双向链表

    ![双向链表](../java/计算机网络/JAVAWEB.assets/bidirectional-linkedlist.png)

  - 双向循环链表

    ![双向循环链表](../java/计算机网络/JAVAWEB.assets/bidirectional-circular-linkedlist.png)

- RandomAccess接口

  ```java
  public interface RandomAccess{
  }
  //什么都没定义，只是一个标识，标签，实现了这个标签说明就有随机访问功能
  ```

  - eg

  ```java
  public static <T>
  int binarySearch(List<? extends Comparable<? super T>> list, T key){
    if(list instanceof RandomAccess || list.size()<BINARYSEARCH_THRESHOLD)
      return Collections.indexedBinarySearch(list, key);
    else
      return Collections.iteratorBinarySearch(list, key);
  }
  //在BinarySearch（）方法中，判断传入的list是否RandomAccess的实例，是的话调用indexedBinarySearch方法，不是的话调用iteratorBinarySearch方法
  ```

  **ArrayList实现了RandomAccess接口，而LinkedList没有实现。和底层有关，ArrayList是数组，天然支持随机访问，时间复杂度为O（1），所以称为快速随机访问。而链表则需要遍历到指定位置才能访问特定元素，时间复杂度为O（N）。**

  - Comparable和Comparator的区别

    Comparable接口和Comparator接口都是Java中用于排序的接口，他们在实现类对象之间比较大小、排序等方面发挥了重要作用

    - Comparable接口实际上是出自java.lang包，他有一个compareTo(Object obj)方法用于排序
    - Comparator接口实际上出自于java.util包，他有一个compare(Object obj1, Object obj2)方法用来排序

- 无序性和不可重复性
  - 无序性不等于随机性，无序性是指存储的数据在底层数组中并非按照数组的索引顺序添加，而是根据数组的哈希值决定的。
  - 不可重复性是指添加元素按照equals（）判断时，返回false，需要同时重写equals（）方法和hashCode（）方法。

- 比较HashSet、LinkedHashSet和TreeSet的不同
  - 三者都是Set接口的实现类，都能保证元素唯一，并且都不是线程安全的
  - HashSet、LinkedHashSet和TreeSet的主要区别在于底层的数据结构不同。HashSet的底层数据结构是哈希表，基于HashMap实现。LinkedHashSet的底层数据结构是链表和哈希表，元素的插入和抽取顺序满足FIFO。TreeSet底层数据结构是红黑树，元素是有序的，排序的方式有自然顺序和定制顺序。
  - 底层数据结构不同导致应用场景不同。HashSet用于不需要保证元素插入和取出顺序的场景，LinkedHashSet用于保证元素的插入和取出顺序满足FIFO的场景，TreeSet用于支持对元素自定义排序的场景。

- Queue和Deque

  - Queue是单端队列，只能从一端插入元素，从另一端删除元素，实现上遵循FIFO原则

  - Queue扩展了Collection接口，因为容量问题而导致操作失败后处理方式的不同，可以分为两类方法：一种在失败后抛出去异常，另一种返回特殊值

    ![Screen Shot 2023-06-09 at 11.38.33 am](../java/计算机网络/JAVAWEB.assets/Screen Shot 2023-06-09 at 11.38.33 am.png)

  - Deque是双端队列，在队列的两端均可以插入或者删除元素
  - Deque扩展了Queue的接口，增加了在队首和队尾进行插入和删除的方法，同样根据失败后的处理方式不同分为两类：

- Map

  - HashMap和Hashtable的区别

    - 线程是否安全：HashMap是非线程安全的，Hashtable是线程安全的，hashtable内部的方法基本都经过synchronized修饰

    - 效率：因为线程安全问题，hashmap效率高一些

    - HashMap可以储存null的key和value，而null作为键只能有一个，null作为值可以有多个。Hashtable不允许有null键值和null value，否则会抛出NullPointerException

    - 初始容量大小和每次扩容容量大小的不同：

      - 创建时如果不指定容量大小，HashTable的默认初始值为11，之后每次扩容，容量变为原来的2n+1.HashMap的默认初始化大小是16.之后每次扩容，容量变为原来的两倍
      - 创建时如果指定了容量大小，Hashtable会直接用，HashMap会扩充为2的幂次方大小

    - 底层数据结构

      JDK1.8之后HashMap在解决哈希冲突的时候有了较大变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树。HashTable没有这样的机制

      **HashMap带有初始容量的构造函数**

      ```java
          public HashMap(int initialCapacity, float loadFactor) {
              if (initialCapacity < 0)
                  throw new IllegalArgumentException("Illegal initial capacity: " +
                                                     initialCapacity);
              if (initialCapacity > MAXIMUM_CAPACITY)
                  initialCapacity = MAXIMUM_CAPACITY;
              if (loadFactor <= 0 || Float.isNaN(loadFactor))
                  throw new IllegalArgumentException("Illegal load factor: " +
                                                     loadFactor);
              this.loadFactor = loadFactor;
              this.threshold = tableSizeFor(initialCapacity);
          }
           public HashMap(int initialCapacity) {
              this(initialCapacity, DEFAULT_LOAD_FACTOR);
          }
      ```

- HashMap和HashSet的区别

  **HashSet底层就是基于HashMap实现的**

  ![Screen Shot 2023-06-11 at 1.55.04 pm](../../java/计算机网络/JAVAWEB.assets/Screen Shot 2023-06-11 at 1.55.04 pm.png)

- HashMap和TreeMap的区别

  **TreeMap和HashMap都继承自AbstractMap，但是TreeMap还实现了NavigableMap接口和SortedMap接口**

  ![TreeMap 继承关系图](../../java/计算机网络/JAVAWEB.assets/treemap_hierarchy.png)

  实现NavigableMap接口让TreeMap有了对集合内元素的搜索能力

  实现SortedMap接口让TreeMap有了对集合内元素根据键排序的能力。默认是按key的升序排列，不过我们也可以指定排序的比较器。
