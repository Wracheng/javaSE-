#### Map

```java
  Map<String,String> map= new HashMap<>();
  //添加一条key、value数据
  map.put("name","zhangsan");
  map.put("age","18");
  // 打印这个map
  System.out.println(map.size()); // 2
  System.out.println(map);
  System.out.println(map.get("name")); // 如果有两个key覆盖掉前面的，找不到是null
  System.out.println(map.keySet()); // 把key转成Set
  System.out.println(map.entrySet()); // [name=zhangsan, age=18] 这个不是数组是Entry类型
  // 三个参数，第二个表示老值,第三个表示新值，返回布尔值,如果第一个参数和第二个参数key和value没匹配上就是false
  System.out.println(map.replace("age","18","19"));
  System.out.println(map.replace("age","19")); // 两个参数表示更新，返回旧的value
  System.out.println(map.containsKey("name")); // 是否包含这个key
  System.out.println(map.containsValue("18")); // 是否包含这个value
  // 遍历Map ==> 转成Set ==> 遍历
  Set<String> set = map.keySet();
  for(String item : set){
      System.out.println("map的key值为======>" + item);
      System.out.println("map的value值为======>" + map.get(item));
  }
  // 优雅遍历Map
  // Set<String,String> set2 = map.entrySet();
  Set<Map.Entry<String,String>> entrySet = map.entrySet(); // Entry是Map里的是一个子接口
  Iterator<Map.Entry<String,String>> it = entrySet.iterator();
  while (it.hasNext()){
      Map.Entry<String,String> item= it.next();
      System.out.println(item);
  }
  // 推荐使用
  for(Map.Entry<String,String> item : entrySet){
    System.out.println(item);
    // Entry类型有获取key和value的能力
    System.out.println(item.getKey());
    System.out.println(item.getValue());
  }
  map.clear(); // 无返回值，map此时变成{},size是0
```
