# 麦克风开发概述

RaScript麦克风模块支持捕获和编码各种常见的音频格式。您可以根据音频使用场景编写能够从设备麦克风捕获音频、保存音频并进行播放的应用。

#### 约束与限制

* 为了能够录制音频，您的应用必须告知用户它将访问设备的音频输入。您需要添加以下权限标记：

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

RECORD\_AUDIO权限可能会对用户的隐私构成威胁。从Android 6.0（API级别23）开始，使用危险权限的应用在运行时必须请求用户的批准。
