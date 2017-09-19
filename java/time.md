Java —— Time
===

### 时间戳 与 毫秒的转换
```
// 当前时间戳
Timestamp timestamp = Timestamp.from(Instant.now());
System.out.println("当前时间戳：" + timestamp);

// 当前毫秒
Long mill = timestamp.getTime();
System.out.println("当前毫秒：" + mill);

// 毫秒数转时间戳
Timestamp timestamp1 = Timestamp.from(Instant.ofEpochMilli(mill));
System.out.println("毫秒转时间戳：" + timestamp1);

// String转时间戳
Timestamp timestamp2 = Timestamp.valueOf("2017-09-19 15:39:40.07");
System.out.println("String转时间戳：" + timestamp2);
```
