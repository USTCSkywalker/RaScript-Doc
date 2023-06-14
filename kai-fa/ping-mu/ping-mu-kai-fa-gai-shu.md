# 屏幕开发概述

RaScript屏幕模块可以实现录屏功能，并且支持设定录制的屏幕帧率、比特率以及录屏时是否启动麦克风。

#### 约束与限制

* 在调用录屏功能前，您需要添加以下权限标记：

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_INTERNAL_STORAGE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```
