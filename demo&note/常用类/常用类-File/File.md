##### File类  
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
###### File的一些静态属性  
```java 
    // 路径分隔符 windows下是; Linux下是:
    System.out.println(File.pathSeparator); // ; 字符串
    System.out.println(File.pathSeparatorChar); // ; 字符
    // 文件名称分隔符   windows下是 \ Linux下是/
    System.out.println(File.separator); // \
    System.out.println(File.separatorChar);
```

##### File的一些判断存在的方法  
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