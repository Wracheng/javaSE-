##### StringBuffer

> final 不可继承
> StringBuffer 类用来处理可变的字符串
> StringBuffer 是线程安全的，不好理解，暂且理解学了线程再理解
> 速度第较快

```java
// 使用length()方法
public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("I Love  ");
      System.out.println(str.length());

    }
}
```
```java
// 使用append()方法
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("I Love");
      // 不得使用 "" + "" 的形式，因为这是String类的小后门
      System.out.println(str.append(" you")); // I Love you
      System.out.println(str.append(15)); // I Love15
  // 与 + 不同的是str从头到尾指向一个地址，而String类型的 + 是新开辟了一个地址存放结果，所以StringBuffer还比String快
    }
}
```
```java
  // 使用insert()方法
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("I Love");
      System.out.println(str.insert(6," You")); // I Love You  位置之前插入字符串
    }
}
```
```java
  // 使用delete()方法
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("I Love");
      System.out.println(str.delete(0,2)); // Love，[0,2)
    }
}
```
```java
  // 使用deleteCharAt()
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝");
      System.out.println(str.deleteCharAt(5)); // 明明很喜欢却又被拒绝
    }
}
```
```java
  // replace
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝");
      System.out.println(str.replace(5, 6,"你")); // 明明很喜欢你却又被拒绝 [5,6)
  }
```
```java
  // reverse()
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝");
      System.out.println(str.reverse()); // 绝拒被又却，欢喜很明明
  }
```
```java
  // setCharAt()
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝");
      str.setCharAt(5,'你'); // 插入一个字符无返回值
      System.out.println(str); // 明明很喜欢你却又被拒绝
  }
```

```java
// capacity()方法  字符数组的长度
public class StudyStringBuffer {
    public static void main(String[] args) {
      // 当有参构造里面是字符串的时候，capacity()的值就是str.length() + 16
      StringBuffer str = new StringBuffer("I Love"); 
      System.out.println(str.capacity()); // str.length() + 16 = 22
      System.out.println(str.append(" youuuuuuuuuuuuuu")); // append()之后capacity()的值就改了
      System.out.println(str.length());
      // 好我们来看一下，append之后str.length()变成了23  23 > 当前的capacity() 22  所以
      System.out.println(str.capacity()); // 2 * 当前的capacity() + 2 = 46
      System.out.println(str.append(" youuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuu"));
      System.out.println(str.length());
      // 好我们来看一下，append之后str.length()变成了95  95 > 当前的capacity() * 2 + 2 = 94 所以
      System.out.println(str.capacity()); // 95
    }
}
```
总结： 设当前的str.capacity()的值为x,最新字符串的长度为y  
* 当 x >= y 时, 最新的x不变;
* 当 x < y 时  
   1、当 y <= x * 2 + 2 时, 最新的x = x * 2 + 2 
   2、当 y > x * 2 + 2 时, 最新的x = y  
**思考**：为什么当x < y时以x * 2 + 2为分界线  
当达到最大容量的时候，就要重新创建一个新的字符数组，并拷贝，所以合理的初始化容量会提升性能
* 最新的capacity()值只跟当前的str.capacity()有关，按上述和设置ensureCapacity()来算都没有capacity()变小的的情况  
```java
  // ensureCapacity()方法
  public class StudyStringBuffer {
    public static void main(String[] args) {
      StringBuffer str = new StringBuffer("I Love");
            System.out.println(str.capacity());
            str.ensureCapacity(47); // 设置capacity的最小值,无返回值
            System.out.println(str.capacity()); // 47
    }
}

public class StudyStringBuffer {
    public static void main(String[] args) {
      // 当有参构造里面是int的时候，capacity()的值就是int值
      StringBuffer str = new StringBuffer(10);
            System.out.println(str.capacity()); // 10
            str.ensureCapacity(6); // 设置capacity的最小值
            System.out.println(str.capacity()); // 10
    }
}
```
总结： 设当前最新的str.capacity()的值为x,ensureCapacity()设置的值为minX
* 当 x >= minX, 最新的 x = x  
* 当 x < minX, 最新的 x = minX  

```java
  // indexOf    
  public class StudyStringBuffer {
    public static void main(String[] args) {
        StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝，我怎敢言喜欢");
        System.out.println(str.indexOf("喜欢", 0)); // 3
        System.out.println(str.indexOf("喜欢", 4)); // 16
    }
}
```
```java
  // charAt    
  public class StudyStringBuffer {
    public static void main(String[] args) {
        StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝，我怎敢言喜欢");
        System.out.println(str.charAt(15)); // 言
    }
}
```
```java
  // lastIndexOf    
  public class StudyStringBuffer {
    public static void main(String[] args) {
        StringBuffer str = new StringBuffer("明明很喜欢，却又被拒绝，我怎敢言喜欢");
        System.out.println(str.lastIndexOf("喜欢")); // 16
    }
}
```
```java
  // getChars copy字符串到char数组中
  public class StudyStringBuffer {
    public static void main(String[] args) {
       String str = new String("明明很喜欢，却又被拒绝，我怎敢言喜欢");
        char[] strChar = new char[6];
        // 从[13,18)截取一段放在strChar中，第四个参数告诉我们首先strChar就被占了1个位置
        str.getChars(13, 18, strChar, 1);
        System.out.println(strChar); // " 怎敢言喜欢"
    }
}
```
思考：为什么可以直接打印数组  println()做了char[]的处理
