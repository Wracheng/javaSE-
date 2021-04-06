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