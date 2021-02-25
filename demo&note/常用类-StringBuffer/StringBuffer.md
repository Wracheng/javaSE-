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
// capacity()方法  StringBuffer的容量
public class StudyStringBuffer {
    public static void main(String[] args) {
      // 当有参构造里面是字符串的时候，capacity()的值就是str.length
      StringBuffer str = new StringBuffer("I Love"); 
      System.out.println(str.capacity()); // str.length() + 16 = 22
      System.out.println(str.append(" youuuuuuuuuuuuuu"));
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
总结： 设当前最新的str.capacity()的值为x,最新字符串的长度为y  
* 当 x <= y 时, 最新的y变成 y;
* 当 x > y 时  
   1、当 x <= y * 2 + 2 时, 最新的y = y * 2 + 2
   2、当 x > y * 2 + 2 时, 最新的y = x


```java
  // ensureCapacity()方法
  public class StudyStringBuffer {
    public static void main(String[] args) {
      // 当有参构造里面是字符串的时候，capacity()的值就是str.length
      StringBuffer str = new StringBuffer("I Love"); 
      System.out.println(str.capacity()); // str.length() + 16 = 22
      System.out.println(str.append(" youuuuuuuuuuuuuu"));
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