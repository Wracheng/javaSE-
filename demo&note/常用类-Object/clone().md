##### (protected) clone()  
> 查看源码 protected native Object clone() throws CloneNotSupportedException 得知以下信息
> protected 子类或同包  
> Object 返回Object类型
> throws CloneNotSupportedException 抛出一个CloneNotSupportedException异常类
> native 暂且理解为其他语言实现
> 思考？为什么要使用clone? 当一个对象过于复杂，使用clone不走构造函数快的一比
```java
// 直接使用Object里的clone()
  public class CloneClass{
    int money = 100;
    CloneClass fn(){
        try {
            CloneClass myclone = (CloneClass) new CloneClass().clone();
            return myclone;
        }catch (Exception e){
            System.out.println(e);
        }
        return null;
    }
}

// myClass

public class MyClass {
    public static void main(String[] args) {
        CloneClass cc = new CloneClass();
        // java.lang.CloneNotSupportedException: com.moxi.demo.CloneClass
        CloneClass cclone = cc.fn();
    }
}

// 主函数就在类中的情况
public class CloneClass{
    int money = 100;
    public static void main(String[] args) {
        CloneClass cc = new CloneClass();
        // java.lang.CloneNotSupportedException: com.moxi.demo.CloneClass
        CloneClass cclone = cc.clone();
    }
}


```

上述结果可知直接使用会抛出一个异常无法使用clone()

``` java
  // 通过实现Cloneable接口让异常消失
  public class CloneClass implements Cloneable{
    int money = 100;
    CloneClass fn(){
        try {
            CloneClass myclone = (CloneClass) new CloneClass().clone();
            return myclone;
        }catch (Exception e){
            System.out.println(e);
        }
        return null;
    }
}

// myClass

public class MyClass {
    public static void main(String[] args) {
        CloneClass cc = new CloneClass();
        CloneClass cclone = cc.fn();
        System.out.println(cc == cclone);
        cclone.money = 30;
        System.out.println(cc.money); // 100 clone()后修改克隆的对象对原对象不影响【目前只试了基本类型】
    }
}

// 主函数就在类中
public class CloneClass implements Cloneable{
    int money = 100;
    public static void main(String[] args) {
        CloneClass cc = new CloneClass();
        // java.lang.CloneNotSupportedException: com.moxi.demo.CloneClass
        CloneClass cclone = cc.clone();
    }
}

// 思考Cloneable为什么能让异常消失？
Cloneable 作为一个标志，表明这个类能被克隆，jvm里会去判断有没有实现这个类来决定抛不抛出异常
```

上述只是作为一个clone()的使用例子，但上述的使用方式太局限了：最大的局限在于由于clone()是Object的protected方法无法在**其他类**的主函数上使用，上述方式不适合使用，于是乎就有了另一种方式重写clone()

```java
  
```