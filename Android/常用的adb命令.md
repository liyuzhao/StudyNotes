# 常用的adb命令

## devices
---
选择一台设备，当只有一台的时候
```
adb shell
```

有多台设备的时候，
```
adb -s devicename shell //devicename: 模式器是ip+port,真机就是设备名
```
## dumpsys
---
打印系统信息的命令
```
adb shell dumpsys ***
```

## meminfo
---
打印进程内存的使用信息
```
adb shell dumpsys meminfo proceName( or PID)
```

## cpuinfo

打印系统CPU的使用信息
```
adb shell dumpsys cpuinfo
```

## intents

获取系统所有intent信息
```
adb shell dumpsys activity intents
```

## broadcasts
获取系统所有 broadcasts 信息
```
adb shell dumpsys activity broadcasts
```

## providers
获取系统所有 providers 信息

```
adb shell dumpsys activity providers
```

## activities
获取系统所有 activities 信息
```
adb shell dumpsys activity activities
```

## processes
获取系统所有processes 信息
```
adb shell dumpsys activity processes
```

## services
获取系统（或指定进程）的所有services信息

```
adb shell dumpsys activity services packagename
```
---
更多的adb命令网站：http://adbshell.com
