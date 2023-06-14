# 构建资源使用场景

#### 步骤一：定义场景函数，如果需要可通过设置场景模式，实现场景自动匹配

{% code lineNumbers="true" %}
```typescript
// 默认的startRecording
@Scenarios
function startRecording() {

}
// EnergySaving, Call场景模式下的startRecording
@Scenarios(EnergySaving, Call)
function startRecording() {

}
// 默认的stopRecording
@Scenarios
function stopRecording() {

}
```
{% endcode %}

#### 步骤二：配置抽象资源

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
    //开启Mic，获取当前录音时⻓
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

#### 步骤三：设置场景使用

{% code lineNumbers="true" %}
```typescript
<template>
    <button @click="startRecording">开始录音</button>
    <button @click="stopRecording">停止录音</button>
</template>
```
{% endcode %}
