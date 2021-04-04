##### toString()

> 不要小看了这个方法，使用频率极其高  
> 基本类型，基本类型是不能调用方法的，我们可以把基本类型通过包装类转成对应的类去调用方法
> 打印 System.out.print / System.out.println 会自动帮我们做这一步

```java
  public class Hongqi extends Computer{

  }
  public class StudyString {
    public static void main(String[] args) {
        // null 是没有toString()的
        // 布尔值
        boolean flag = true;
        System.out.println(flag.toString()); //Cannot resolve method 'toString()'
        // 布尔值对应的包装类是Boolean,Boolean类重写了toString方法
        Boolean flag = true
        System.out.println(flag.toString()); // "true"
        // 整数 已经说过基本类型是不支持调用方法的，所以整数也有对应的包装类
        Integer num = 5;
        System.out.println(num.toString()); // "5"
        // 浮点数
        Float num = -1.5f;
        System.out.println(num.toString()); // "-1.5"
        // 数组
        int[] arr = new int[5];
        // 本质上是arr.toString()
        System.out.println(arr); // 打印[I@4554617c
        System.out.println(Arrays.toString(arr)); // [0, 0, 0, 0, 0, 0]
        // 对象  本质上是new Hongqi().toString()
        System.out.println(new Hongqi()); // com.moxi.demo.Hongqi@74a14482 打印对象的完整信息
      }
}
```
对于对象打印这个玩意不合适,我们可以重写toString()来达到我们想要输出的结果

```java
  public class Hongqi extends Computer{
    @Override
    public String toString() {
        return "输出红旗飘扬";
    }
  }
  
  public class StudyString {
    public static void main(String[] args) {
        System.out.println(new Hongqi()); // 输出红旗飘扬
      }
}
  
```
