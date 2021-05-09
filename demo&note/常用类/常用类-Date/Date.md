##### Date  日期类
```java
  // 可以传一个毫秒数注意这个毫秒数可能很大所以是long类型
  Date d = new Date();
  // 获取时间的毫秒数
  System.out.println(d.getTime());
  // Date的子类 java.sql.Date
  java.sql.Date sqlDate = new java.sql.Date(System.currentTimeMillis());
  System.out.println(sqlDate); // 2021-05-09
  // 将字符串（2021-05-09这种用"-"连接的字符串年月日，其中月日可以不带0前缀）转换成java.sql.Date
  java.sql.Date sqlDate2 = java.sql.Date.valueOf("2021-05-09");
  System.out.println(sqlDate2); // 2021-05-09
```

##### DataFormat抽象类 （用于Date和模板字符串之间的转换）
```java
  // 将自己所需要的字符串日期格式变成Date
  String str = "2021-05-09 16:30:00";
  DateFormat dfs = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
  Date date = dfs.parse(str);
  String s = dfs.format(date);
```

##### Calendar抽象类 代替Date里的getYear()、getMonth()、getDate()等方法
```java
  // calendar 一般用获取设置年月日的,功能比较多
  Calendar calendar = new GregorianCalendar();
  System.out.println(calendar);
  Calendar calendar = new GregorianCalendar();
  System.out.println(calendar);
  System.out.println(calendar.get(Calendar.YEAR)); // 2021
  System.out.println(calendar.get(Calendar.MONTH)); // 4  (5月)
  System.out.println(calendar.get(Calendar.DATE));  // 9
  System.out.println(calendar.get(Calendar.DAY_OF_MONTH)); // 9
  System.out.println(calendar.get(Calendar.DAY_OF_WEEK)); // 1 (星期日 从1开始，代表一周第几天)
  System.out.println(calendar.get(Calendar.HOUR)); // 5 (12小时制)
  System.out.println(calendar.get(Calendar.HOUR_OF_DAY)); // 17 (24小时制)
  System.out.println(calendar.get(Calendar.MINUTE)); // 21
  System.out.println(calendar.get(Calendar.SECOND)); // 58
  System.out.println(calendar.getActualMaximum(Calendar.DATE)); // 该月最大多少天
  // 设置日期
  calendar.set(Calendar.DATE,1); // 将日设为1号
  calendar.add(Calendar.DATE,1); // 将日加一天
```

##### 以前的时间处理类不支持时区、线程不安全
```java
  // jdk1.8 处理时间
  
  // 获取当前时间
  LocalDateTime localDateTime = LocalDateTime.now();
  System.out.println(localDateTime.getDayOfYear()); // 一年中第几天
  System.out.println(localDateTime.getDayOfMonth()); // 月中第几天
  System.out.println(localDateTime.getDayOfWeek()); // "SUNDAY" 星期几

  // 获取指定的时间 LocalDateTime.of (特别的：month从1开始)
  LocalDateTime localDateTime2 = LocalDateTime.of(1111,12,12,12,12,12);
  System.out.println(localDateTime2);

  // 格式化时间
  String timeStr = "1997-10-10 10:00:00";
  DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
  LocalDateTime localDateTime1 = LocalDateTime.parse(timeStr,dtf); // timeStr以dtf的格式解析
  System.out.println(localDateTime1);
  String timeStr2 = localDateTime1.format(dtf);
  System.out.println(timeStr2);
```