# 场景自适应

用户在调用场景函数时，系统会根据全局的场景模式状态表，自动匹配符合当前的场景模式的场景函数，进行执行。

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
    // 开启Mic，获取当前录音时⻓
    Mic(mic_start).onOriginData((result: any) => {
        setRecordTime(result);
    });
}
// 用户调用startRecording()时，会根据全局的场景模式状态表，自动匹配符合要求的startRecording
startRecording();
```
{% endcode %}
