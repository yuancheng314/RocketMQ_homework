﻿# 数据来源
[数据](https://github.com/apache/rocketmq-streams/blob/main/rocketmq-streams-examples/src/main/resources/data.txt)
```
{"InFlow":"1","ProjectName":"ProjectName-0","LogStore":"LogStore-0","OutFlow":"0"}
{"InFlow":"2","ProjectName":"ProjectName-1","LogStore":"LogStore-1","OutFlow":"1"}
{"InFlow":"3","ProjectName":"ProjectName-2","LogStore":"LogStore-2","OutFlow":"2"}
{"InFlow":"4","ProjectName":"ProjectName-0","LogStore":"LogStore-0","OutFlow":"3"}
{"InFlow":"5","ProjectName":"ProjectName-1","LogStore":"LogStore-1","OutFlow":"4"}
{"InFlow":"6","ProjectName":"ProjectName-2","LogStore":"LogStore-2","OutFlow":"5"}
{"InFlow":"7","ProjectName":"ProjectName-0","LogStore":"LogStore-0","OutFlow":"6"}
{"InFlow":"8","ProjectName":"ProjectName-1","LogStore":"LogStore-1","OutFlow":"7"}
{"InFlow":"9","ProjectName":"ProjectName-2","LogStore":"LogStore-2","OutFlow":"8"}
{"InFlow":"10","ProjectName":"ProjectName-0","LogStore":"LogStore-0","OutFlow":"9"}
```
## 处理
输出
```
class FileSourceExample {
    public static void main(String[] args) {
       DataStreamSource source = StreamBuilder.dataStream("namespace", "pipeline");
        source.fromFile("source.txt", true)
                .map(message -> message)
                .filter(message -> ((JSONObject)message).getInteger("InFlow") > 4 && ((JSONObject)message).getString("LogStore").equals("LogStore-0"))
                .map(message -> ((JSONObject) message).getString("ProjectName"))
                .toFile("./result.txt")
                .start();
    }
}
```

结果为
```
ProjectName-0
ProjectName-0
```
