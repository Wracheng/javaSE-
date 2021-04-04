```java
public class demo3 {
    public static void main(String[] args) {
        Person p = new Person(23, "zhang");
        Class pclass = p.getClass();
        System.out.println(pclass); // 如果Person是和demo3这个类同包直接返回类名，不同包返回带包路径的类名
        //getName()获取虚拟机类名, getCanonicalName(): 返回权威的类名, 当为匿名类时, getCanonicalName返回输出的是null,classSimpleName返回"",classSimpleName肯定不带包路径名
        //带不带包名是要打印的类名看是不是同包的，是就不带，不是就带
        //对于数组：比如int[]
        // getName()返回的是：[I
        // getCanonicalName()返回的是：int[]

        // 对于内部类：
        // getName()返回的是：com.getname.pkg.Main$Demo1$Demo2
        // getCanonicalName()返回的是：com.getname.pkg.Main.Demo1.Demo2
        String className = pclass.getName();
        String classCanonicalName = pclass.getCanonicalName();
        String classSimpleName = pclass.getSimpleName();
        System.out.println("className:" + className +","+"classCanonicalName:"+classCanonicalName,"classSimpleName:" + classSimpleName);
        System.out.println(pclass.getDeclaredMethod("getAge")); // public int Person.getAge() 从类本身上找
        System.out.println(pclass.getMethod("getAge")); // public int Person.getAge() 会从祖先上找
        //常用的有如下:
        // getFields：获取public修饰的所有属性，返回一个Field数组（包括父类的）
        // getDeclaredFields：获取所有属性，返回一个Field数组
        // getField：传入一个参数（属性名），获取单个属性，返回一个Field对象，只能获取public修饰的
        // getDeclaredField：传入一个参数（属性名），获取单个属性，返回一个Field对象
        // getMethods：获取所有的public修饰的方法，包括父类的，返回Method
        // getDeclaredMethods：获取所有的返回，不包括父类，返回Method数组
        // getMethod：传入一个参数（方法名），返回一个Method对象，只能获取到public修饰的
        // getDeclared：传入一个参数（方法名），返回一个Method对象
        // newInstance：创建该类型的一个实例
    }
}

```
