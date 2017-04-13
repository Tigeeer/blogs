Java —— String
===

### 分割字符串，获得最后一个字符串

**使用split**
```
String str = arr.split("_")[arr.split("_").length()-1]
```

**使用subString，（PS:如果关键字不存在，lastIndexOf返回-1，抛出异常）**
```
String str = arr.subString(arr.lastIndexOf("_"));
```
