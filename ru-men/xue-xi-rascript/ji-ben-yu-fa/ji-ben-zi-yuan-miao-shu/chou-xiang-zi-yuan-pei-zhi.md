# 抽象资源配置

不同抽象资源的静态属性和抽象动作种类需参考对应的抽象资源管理类文档，并进行链式设置。其中，静态属性可以通过属性对象一次性设置，也可以通过链式调用逐个设置。

{% code lineNumbers="true" %}
```typescript
// 设置静态属性对象：sensor_start
Sensor(sensor_start);
Sensor({ sensorType: "accelerometer", operation: ["start"] });
// 链式设置静态属性
Sensor().sensorType("accelerometer").operate(["stop"]);
```
{% endcode %}

如果需要，可以设置回调函数，进行自定义处理：

{% code lineNumbers="true" %}
```typescript
Sensor().sensorType("accelerometer").operate(["get_curdata"]).onGetData((result: any) => {
    console.log("回调了：" + "x: " + result.x);
});
```
{% endcode %}
