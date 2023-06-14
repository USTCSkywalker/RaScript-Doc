# 编译执行

#### 编译前：

{% code lineNumbers="true" %}
```typescript
// 默认的startRecording
@Scenarios
function startRecording() {
    // 开启Mic，获取当前录音时⻓
    Mic(mic_start).onOriginData((result: any) => {
        setRecordTime(result);
    });
    // 开启位置监听，获取当前位置
    Location().operate(["continuous"]).onOriginData((result: any) => {
        setLocation(result);
    });
}
// EnergySaving, Call场景模式下的startRecording
@Scenarios(EnergySaving, Call)
function startRecording() {
    // 开启Mic，获取当前录⾳时⻓
    Mic(mic_start).onOriginData((result: any) => {
        setRecordTime(result);
    });
}
// 默认的stopRecording
@Scenarios
function stopRecording() {
    Mic(mic_local).operate(["stop", "get_lastdata"]).onGetData((result: any) => {
    });
}
```
{% endcode %}

#### 编译后：

{% code lineNumbers="true" %}
```typescript
// 默认的startRecording
function startRecording_default() {
    // 开启Mic，获取当前录音时⻓
    Mic.getInstance().attr(new mic_start()).onOriginData(function (result) {
        setRecordTime(result);
    }).build();
    // 开启位置监听，获取当前位置
    Location.getInstance().operate(["continuous"]).onOriginData(function(result) {
        setLocation(result);
    }).build();
}
// EnergySaving, Call场景模式下的startRecording
function startRecording_EnergySaving_Call() {
    // 开启Mic，获取当前录音时⻓
    Mic.getInstance().attr(new mic_start()).onOriginData(function (result) {
        setRecordTime(result);
    }).sceAttr(new EnergySaving(), new Call()).build(); }
// 默认的stopRecording
function stopRecording_default() {
    Mic.getInstance().attr(new mic_local()).operate(["stop", "get_lastdata"]).onGetData(function (result) {
    }).build();
}
function startRecording() {
    if (EnergySaving.state && Call.state) {
        startRecording_EnergySaving_Call();
        return;
    }
    startRecording_default();
}
function stopRecording() {
    stopRecording_default();
}
```
{% endcode %}

#### 编译后新增代码

{% code lineNumbers="true" %}
```typescript
1.通用的重复代码：
getInstance(), attr(), new, build(), sceAttr()

2.场景模式自适应匹配函数
function startRecording() {
    if (EnergySaving.state && Call.state) {
        startRecording_EnergySaving_Call();
        return;
    }
    startRecording_default();
}
function stopRecording() {
    stopRecording_default();
}
```
{% endcode %}
