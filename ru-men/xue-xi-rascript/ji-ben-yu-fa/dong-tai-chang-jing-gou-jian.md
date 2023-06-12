# 动态场景构建

RaScript提供在@Scenarios装饰的场景描述函数中，根据使用需求，定义⼀种或多种抽象资源，并进行描述的能力。用户可以根据具体需求自由组合抽象资源，并使用数据处理提供的方式，进行资源数据交互。

{% code lineNumbers="true" %}
```typescript
@Scenarios
function stopRecording() {
    let recodingFile = "";
    let position1 = "";
    // Mic组件：停止录音，获取⽂件路径数据
    Mic(mic_local).operate(["stop", "get_lastdata"]).onGetData((result: any) => {
        recodingFile = result;
        console.log("回调了当前录⾳路径：" + recodingFile);
    });
    // 位置组件：停止位置监听，获取最近一次位置信息
    Location().operate(["stop", "get_lastPos"]).onGetData((result: any) => {
        position1 = JSON.stringify(result);
    });
    // 存储组件：存储到DB
    Storage(storage_insert).onInsert(() => {
        console.log("回调了：插⼊函数");
        return {
            path: recodingFile,
            position: position1
        }
    });
}
```
{% endcode %}
