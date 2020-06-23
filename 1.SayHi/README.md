# 根据不同的时间段，输出不同的问候

```
早上好: 05:01-08:59
上午好: 09:00-12:00
中午好: 12:01-13:59
下午好: 14:00-18:59
晚上好: 19:00-23:59
凌晨好: 00:00-05:00
```

要求用Java实现这个需求。

下面是实现的代码片段

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.*;

public static void main(String[] args) {
    System.out.println("hello");

    String timeStr = LocalDateTime.now().format(DateTimeFormatter.ofPattern("HH:mm"));
    System.out.println(timeStr);
    String monningPattern = "05:(0[1-9]|[1-5][0-9])|0[6-8]:..";
    String amPattern = "09:..|1[01]:..|12:00";
    String noonPattern = "12:(0[1-9]|[1-5][0-9])|13:..";
    String pmPattern = "1[4-8]:..";
    String eveningPattern = "19:..|2[0-3]:..";
    String weePattern = "0[0-4]:..|05:00";
    Map<String,String> patternMap = new HashMap<>();
    
    patternMap.put("早上好",monningPattern);
    patternMap.put("上午好",amPattern);
    patternMap.put("中午好",noonPattern);
    patternMap.put("下午好",pmPattern);
    patternMap.put("晚上好",eveningPattern);
    patternMap.put("凌晨好",weePattern);
    patternMap.forEach((k,v)->{
        Pattern compile = Pattern.compile(v);
        Matcher matcher = compile.matcher(timeStr);
        if(matcher.find()){
            System.out.println(k);
            return;
        }
    });
}
```