#### HashSet 
```java
  public class HashSet1 {
    public static void main(String[] args) {
        Set<String> set = new HashSet();
        Set<Integer> set2 = new LinkedHashSet();
        Set<String> set3 = new TreeSet();
        set.add("569");
        set.add("hello");
        set.add("123");
        set.add("hello2");
        set.add("123");
        System.out.println(set); // [123, 569, hello2, hello] 无序、唯一
        set2.add(123);
        set2.add(234);
        set2.add(124);
        set2.add(124);
        System.out.println(set2); // [123, 234, 124]  有序、唯一
        set3.add("zz");
        set3.add("javaSE");
        set3.add("JavaSE");
        set3.add("JavaSE");
        System.out.println(set3); // [JavaSE, javaSE, zz]  按大小有序，唯一

        // 遍历除了for形式，其他三种都能用，因为Set没有index
    }
}
```