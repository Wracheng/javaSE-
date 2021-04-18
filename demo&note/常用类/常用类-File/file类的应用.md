##### 递归打印多级目录  
```java
   public class studyFile {
    public static void main(String[] args){
        File file = new File("D:\\soft\\Apipost");
        // static 里只能调用static方法。
        readFiles(file);
    }
    public static void readFiles(File file){

        File[] fileList = file.listFiles();
        for( File item : fileList){
            System.out.println(item.isDirectory());
            if(item.isDirectory()){
                readFiles(item);
            }else{
                System.out.println(item);
            }
        }

    }
}
```  
##### 递归打印多级目录中指定文件(这里以.java后缀举例)  
```java
       public class studyFile {
    public static void main(String[] args){
        File file = new File("D:\\soft\\Apipost");
        // static 里只能调用static方法。
        readFiles(file);
    }
    public static void readFiles(File file){

        File[] fileList = file.listFiles();
        for( File item : fileList){
            if(item.isDirectory()){
                readFiles(item);
            }else{
                // 只是多了一个判断 toLowerCase()是为了兼容后缀名大小写
                if(item.getName().toLowerCase().endsWith(".java")){
                    System.out.println(item);
                }
            }
        }

    }
}
```