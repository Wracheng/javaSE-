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
    // equalsIgnoreCase 比较两个字符串的内容（忽略大小写）
    public class StudyString {
    public static void main(String[] args) {
        String str1 = new String("abcd");
        String str2 = new String("aBCd");
        System.out.println(str1.equalsIgnoreCase(str2)); // true
    }
}
```
```java
    // trim() 去掉两边空格
    public class StudyString {
    public static void main(String[] args) {
        String str = new String(" abcd ");
        System.out.println(str.trim()); // abcd
    }
}
```
```java
    // substring() 截取字符串 (通用，返回String类型)
    public class StudyString {
    public static void main(String[] args) {
        String str = new String(" abcd ");
        System.out.println(str.substring(0)); // abcd
        System.out.println(str.substring(1)); // bcd
        System.out.println(str.substring(0,2)); // ab
        StringBuffer str1 = new StringBuffer("abcd");
        String s = str1.substring(0,2); // 很容易在这出错
        System.out.println(s); // ab
    }
}
```
```java
    // contains 字符串是否包含另一个字符串
    public class StudyString {
    public static void main(String[] args) {
        String str = new String("abcd");
        System.out.println(str.contains("cd")); // true
        System.out.println(str.contains("")); // true
    }
}
```
```java
    // startsWith、endsWith
    public class StudyString {
    public static void main(String[] args) {
        String str = new String("abcd");
        System.out.println(str.startsWith("ab")); // true
        System.out.println(str.endsWith("d")); // true
    }
}
```
```java
    // replace、replaceFirst、replaceAll  String的replace和StringBuffer的replace用法不同
    public class StudyString {
    public static void main(String[] args) {
        String str = "abcdabcdabcd";
        System.out.println(str.replace("ab","xx")); // xxcdxxcdxxcd  全部符合条件的替换,这与js不同
        System.out.println(str.replace('a','x')); // xbcdxbcdxbcd 前后都为字符
        System.out.println(str.replaceFirst("ab","xx")); // xxcdabcdabcd
        System.out.println(str.replaceAll("a","x")); // xbcdxbcdxbcd 但要注意第一个参数是正则不是字符串
        System.out.println(str.replaceAll("good","x")); // abcdabcdabcd 没匹配上返回原字符串
    }
}
```