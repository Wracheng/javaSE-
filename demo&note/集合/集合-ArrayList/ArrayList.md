#### ArrayList

```java
  public class ArrayList2 {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList();  // 默认是0,   new ArrayList(1000);这并不会使得size()发生变化,只是数组扩容机制和StringBuffer相似，每次扩容1.5倍,如果1.5倍不够，就取够得最小值。
        List<Integer> list2 = new ArrayList();
        list.add(8); // 添加一个元素
        list.add(0,1); // 指定位置添加元素
        list.set(0,2); // set只能对存在的值做修改所以,当前值必须有值
        System.out.println(list.isEmpty());
        System.out.println(list.contains(2));
        list.remove(1); // 删除指定位置的元素
        list.remove(Integer.valueOf(2)); // 通过值删除元素，注意要包装一下，不然会误认为是下标,只会删除第一次出现的
        list.clear(); // 清空
        System.out.println(list);
        list.add(100);
        list2.add(1);
        list2.add(2);
        list2.add(1);
        list2.add(3);
        list.addAll(list2); // 两个ArrayList拼接list2拼在list后面
        list.addAll(0,list2); // index范围0 - size() 拼接在指定位置后面
        System.out.println(list);
        System.out.println(list2);
        list.removeAll(list2); // 在list中删除所有list2中所有的元素
        list.retainAll(list2); // 在list中留下所有list2中所有的元素
        list.replaceAll(item -> item + 1); // 将所有元素 + 1  当然这还有特别几个元素处理的功能
        System.out.println(list);

        // ----------------------------四大遍历
        // for遍历 size()底层还是用到了数组的length方法,区别在于size是有值的空间的个数list.add(null)是size()算1个
        for(int i = 0; i < list.size(); i++){
            System.out.println(list.get(i)); // 如果没有泛型则需要 int item = (int) list.get(i); 因为返回的是Object类型，其实这里是先转成Integer,再拆包
        }
        // for-each遍历
        for (Integer value: list) {
            System.out.println(value);
        }
        // 迭代器遍历
        Iterator<Integer> it = list.iterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }
        // lambda表达式
        // 常规写法
        list.forEach((item) -> System.out.println(item));
        // 精简写法
        list.forEach(System.out::println);
    }
}
```
