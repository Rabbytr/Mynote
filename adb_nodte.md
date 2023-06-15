连接手机

比如mumu模拟器：

```shell
adb connect 127.0.0.1:7555
```

查询和设置Android ID：

```shell
adb shell settings get secure android_id
adb shell settings put secure android_id [android_id]
```

更多详见[adb-awesome](https://github.com/mzlogin/awesome-adb)