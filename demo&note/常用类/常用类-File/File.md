##### File 类

```java
// 构造方法
public class studyFile {
    public static void main(String[] args) {
        // 值得一提的是Linux是 / windows是 \, \的时候需要转义
        // File里的路径不管存不存在都行，因为只是路径封装成File对象
        File file1 = new File("P:\\ts\\a.ts");
        System.out.println(file1); // P:\ts\a.ts
        File file2 = new File("P:\\ts\\"); // P:\ts
        System.out.println(file2);
        // a.txt 也可以直接写文件名,此时是相对路径，相对于当前根路径
        File file3 = new File("a.txt");
        System.out.println(file3);

    }
}

public class studyFile {
    public static void main(String[] args) {
        public static void main(String[] args) {
        // 把路径分成了两部分,好处是灵活
        File file1 = new File("P", "ts\\a.ts");
        System.out.println(file1); // P\ts\a.ts

    }
  }

  public class studyFile {
    public static void main(String[] args) {
        // 把路径分成了两部分,好处是灵活,并且第一个参数是File类型能用File的一些方法
        File file = new File("P", "ts\\a");
        File file1 = new File(file, "b.txt");
        System.out.println(file1); // P\ts\a\b.txt

    }
}
```

###### File 的一些静态属性

```java
    // 路径分隔符 windows下是; Linux下是:
    System.out.println(File.pathSeparator); // ; 字符串
    System.out.println(File.pathSeparatorChar); // ; 字符
    // 文件名称分隔符   windows下是 \ Linux下是/
    System.out.println(File.separator); // \
    System.out.println(File.separatorChar);
```

##### File 的一些判断存在的方法

```java
    // 判断文件夹或文件是否存在
    public static void main(String[] args) {
        File file = new File("D:\\soft\\HBuilderX");
        File file2 = new File("D:\\soft\\HBuilderX\\HBuilderX.exe");
        File file3 = new File("D:\\soft\\HBuilder");
        System.out.println(file.exists()); // true
        System.out.println(file2.exists()); // true
        System.out.println(file3.exists()); // false
    }
    // 判断是不是目录  不存在和文件返回false
    File file = new File("D:\\soft\\HBuilderX");
    File file2 = new File("D:\\soft\\HBuilderX\\HBuilderX.exe");
    File file3 = new File("D:\\soft\\HBuilder");
    System.out.println(file.isDirectory()); // true
    System.out.println(file2.isDirectory()); // false
    System.out.println(file3.isDirectory()); // false
    // 判断是不是文件  不存在和文件夹返回false
    File file = new File("D:\\soft\\HBuilderX");
    File file2 = new File("D:\\soft\\HBuilderX\\HBuilderX.exe");
    File file3 = new File("D:\\soft\\HBuilder");
    System.out.println(file.isFile()); // false
    System.out.println(file2.isFile()); // true
    System.out.println(file3.isFile()); // false

    注意： new File("a.txt") // 这是相对于src文件夹下的
```

###### 文件/文件夹的创建

```java
    public static void main(String[] args)  {
        File file = new File("Demo2.java");
        // 创建有两个要求 1、路径必须存在，不然抛出异常 2、不能创建文件夹 3、构造参数里没有带后缀也能创建文件
        try {
            Boolean f = file.createNewFile();
            System.out.println(f);
        } catch (IOException e) {
            System.out.println("??");
            e.printStackTrace();
        }

    }
```

```java
    public static void main(String[] args)  {
       File file = new File("D:\\安装包\\a\\bb");
       // 创建的路径不存在不是抛出异常是返回false,文件夹已经存在返回false
       System.out.println(file.mkdir()); // false 只可以创建单级
       System.out.println(file.mkdirs()); // true 可以创建单级和多级
       File file2 = new File("D:\\安装包\\a.txt");
       System.out.println(file.mkdir()); // true  此时的文件夹名就是a.txt

    }
```

###### 文件/文件夹的删除

```java
    // delete 不走回收站，文件夹内有文件返回false,路径不存在返回false,删不掉
    File file = new File("D:\\安装\\a");
    System.out.println(file.delete()); // true
```

###### 遍历文件/文件夹

```java
    // String[] list()  遍历文件/文件夹,包括隐藏文件 路径不存在或不是一个文件夹路径会抛出异常
    // File[] listFiles() 遍历文件/文件夹,包括隐藏文件 路径不存在或不是一个文件夹路径会抛出异常
    public static void main(String[] args) throws IOException {
        File file = new File("D:\\myWebpack");
        System.out.println(Arrays.toString(file.list())); //[.nojekyll, index.html, README.md, webpack初体验, _navbar.md, _sidebar.md] // 带后缀的
        System.out.println(Arrays.toString(file.listFiles())); //[D:\myWebpack\.nojekyll, D:\myWebpack\index.html, D:\myWebpack\README.md, D:\myWebpack\webpack初体验, D:\myWebpack\_navbar.md, D:\myWebpack\_sidebar.md]

    }
```

###### 通过文件过滤接口去优化（其实是减少 listFiles 的输出去减少优化递归遍历的次数）

```java
    // 1、listFiles方法是会去调用实现FileFilter接口的accept方法的 ★
    // 2、listFiles的参数是一个实例（实现了接口的）
    // 3、accept方法返回true的才会返回到File[]中
    // 找出一个P:\javaEE\src下的所有.java文件

// FileFilter接口
public class FileSearch implements FileFilter {
    public static void main(String[] args) {
        // 首先找到文件夹
        File file = new File("P:\\javaEE\\src");
        // 然后去遍历
        readFiles(file);
    }

    public static void readFiles(File file){

        File[] fileList = file.listFiles(new FileSearch()); // 这里的FileSearch其实就是实现了FileFilter接口的类
        for( File item : fileList){
            if(item.isDirectory()){
                readFiles(item);
            }else{
                System.out.println(item);
            }
        }

    }

    @Override
    public boolean accept(File pathname) {
        // 别忘了处理文件夹的情况
        return pathname.isDirectory() || pathname.getName().toLowerCase().endsWith(".java");
    }

}

// 实现FilenameFilter 接口
public class FileSearch implements FilenameFilter {
    public static void main(String[] args) {
        // 首先找到文件夹
        File file = new File("P:\\javaEE\\src");
        // 然后去遍历
        readFiles(file);
    }

    public static void readFiles(File file){

        File[] fileList = file.listFiles(new FileSearch()); // 这里的FileSearch其实就是实现了FilenameFilter接口的类
        for( File item : fileList){
            if(item.isDirectory()){
                readFiles(item);
            }else{
                System.out.println(item);
            }
        }

    }

    @Override // 其实就是把FilenFilter的参数拆成了两个一个是文件夹一个是文件夹里的文件(夹)名
    public boolean accept(File dir, String name) {
        return new File(dir,name).isDirectory() || name.toLowerCase().endsWith(".java");
    }
}
```  

使用Lambda表达式
```java
    // 表示一个类的实例,这个实例需要满足实现的接口内只有一个抽象方法 【类似于ES6的箭头函数】
    // File[] fileList = file.listFiles(new FileSearch())
    //                     ↓

    // 实现FilenFilter
    File[] fileList = file.listFiles( filename -> pathname.isDirectory() || pathname.getName().toLowerCase().endsWith(".java"))
    // 实现FilenameFilter
    File[] fileList = file.listFiles( dir,name -> new File(dir,name).isDirectory() || name.toLowerCase().endsWith(".java"))
```

还可以用匿名内部类的形式
```java
    // 实现FileFilter
    File[] fileList = file.listFiles(new FileSearch(){
      @Override
      public boolean accept(File filename) {
      return filename.isDirectory() || filename.toLowerCase().endsWith(".java");
      }
    })
    // 实现FilenameFilter
    File[] fileList = file.listFiles(new FileSearch(){
      @Override
      public boolean accept(File dir, String name) {
      return new File(dir,name).isDirectory() || name.toLowerCase().endsWith(".java");
      }
    })
```
