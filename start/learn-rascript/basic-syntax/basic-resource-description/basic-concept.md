# 基本概念

* 装饰器：装饰器给被装饰的对象赋予某一种能力，其不仅可以装饰函数，还可以装饰变量。
* @Scenarios：装饰function，function在装饰后具有管理资源的能力，编译器会根据@Scenarios对场景内的抽象资源进行构建和调⽤。@Scenarios后可以输入参数指定“场景模式”，如 Call：通话模式；EnergySaving：节能模式。
* 链式调用：抽象资源的静态属性和抽象动作可以通过链式调用的形式进行设置。&#x20;
* 省略getInstance()，attr()，new，build()，sceAttr()重复代码。

RaScript开发范例如下：

{% code lineNumbers="true" %}
```typescript
// @Scenarios⽆参形式：表示默认的startRecording
@Scenarios
function startRecording() {
    // 使用Mic组件：省略getInstance(),attr(),new,build(),sceAttr()等代码；
    // 此处表示：开启Mic，获取当前录音时⻓
    Mic(mic_start).onOriginData((result: any) => {
        setRecordTime(result);
    });
    // 开启位置监听，获取当前位置
    Location().operate("continuous").onOriginData((result: any) => {
        setLocation(result);
    });
}
// @Scenarios有参形式：表示EnergySaving及Call场景模式同时为true时的startRecording
@Scenarios(EnergySaving & Call)
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
