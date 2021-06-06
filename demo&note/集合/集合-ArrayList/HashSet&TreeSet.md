#### HashSet 和 TreeSet
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
```java
// 存类的问题
public class HashSet2 {
    public static void main(String[] args) {
        Set<Student> set = new HashSet<Student>();
        Student s = new Student("wrang",85,24);
        Student s2 = new Student("pan",100,24);
        Student s3 = new Student("fang",99,25);
        Student s4 = new Student("wrang",85,24);
        set.add(s);
        set.add(s2);
        set.add(s3);
        set.add(s4);
        // 可知有4个，但是本意是s和s4是一样的，由于唯一性应该只保留s才对，现在都保留是因为equals()和hashCode()方法还没有重写导致类的比较采用内部比较
        // 要比较两个类equals()和hashCode()都要重写缺一不可
        // String没有这个问题是因为系统类已经处理了
        for(Student x : set){
            System.out.println(x.toString());
        }
        // 这是添加顺序，没什么好说的
        Set<Student> linkedHashSet = new LinkedHashSet<>();
        // 这是红黑树，需要用到内容比较，那么问题就来了，怎么比 继承Comparable,重写compareTo方法，顺带一提Comparable只有一个抽象类compareTo方法所以可以使用λ表达式
        Set<Student> treeSet = new TreeSet<Student>((stu1,stu2)-> {
            if(stu1.getAge() - stu2.getAge() > 0){
                return 1;
            }else if(stu1.getAge() - stu2.getAge() < 0){
                return -1;
            }else{
                return 0;
            }
        });
        treeSet.add(s);
        treeSet.add(s2);
        treeSet.add(s3);
        treeSet.add(s4);
        for(Student x : treeSet){
            System.out.println(x.toString());
        }
    }

}
```
```java
// 哈希表的原理
```