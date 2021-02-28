##### String  
> String类是final的，不可改变

```java
   public class StudyString {
    public static void main(String[] args) {
        String str = "I Love You";
        str = "Really?";
        System.out.println(str); // Really?  这明明是更改了啊？
        // 流程如下： 1、创建一个"I Love You"的对象 str指向他
        // 2、又创建一个"Really?"对象 str去指向他
        // 3、清除原先的"I Love You"的对象
    }
}
```
思考: String str = "I Love You" 和  String str = new String("I Love You")的区别  
```java
    public class StudyString {
    public static void main(String[] args) {
        String str1 = "我想死你们了";
        String str2 = "我想死你们了";
        String str3 = new String("我想死你们了");
        System.out.println(str1 == str2); // true  因为str1和str2都指向了同一个地址
        System.out.println(str1 == str3); // false 因为new 是又重新开辟了一个空间str3指向那块空间地址不一样了
    }
}
```
来看一下String的常见方法
```java
    // 取出第几个字符charAt (共用)
    public class StudyString {
    public static void main(String[] args) {
        String str1 = "我想死你们了";
        System.out.println(str1.charAt(0)); // 我
        System.out.println(Arrays.toString(str1.toCharArray())); // [我,想,死,你,们,了]
    }
}
```
```java
    // toUpperCase 
    public class StudyString {
    public static void main(String[] args) {
        String str1 = "abcd";
        System.out.println(str1.toUpperCase()); // ABCD
    }
}
```
```java
    // split
    public class StudyString {
    public static void main(String[] args) {
        String str = new String("abcd");
        String[] strArr = str.split(":");
        System.out.println(strArr[0]); // abcd
    }
}
```
```java
    // equals 比较两个字符串的内容（StringBuffer能用但是没重写，不能比较内容）
    public class StudyString {
    public static void main(String[] args) {
        String str1 = new String("abcd");
        String str2 = new String("abcd");
        System.out.println(str1.equals(str2)); // true
    }
}
```
```java
    // trim() 去掉两边空格
    public class StudyString {
    public static void main(String[] args) {
        String str1 = new String(" abcd ");
        System.out.println(str1.trim()); // abcd
    }
}
```
```java
    // substring() 去掉两边空格
    public class StudyString {
    public static void main(String[] args) {
        String str1 = new String(" abcd ");
        System.out.println(str1.trim()); // abcd
    }
}
```