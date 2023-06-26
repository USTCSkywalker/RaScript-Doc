# 传感器开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
//开启sensor
@Scenarios
function sensorStart() {
    //设置静态属性对象
    Sensor({ sensorType: "accelerometer", operation: ["start"] });
}
//停止sensor
@Scenarios
function sensorStop() {
    //链式设置静态属性
    Sensor().sensorType("accelerometer").operate(["stop"]);
}
//获取数据
@Scenarios
function sensorGetData() {
    //链式设置静态属性和回调函数
    Sensor().sensorType("accelerometer").operate(["get_curdata"]).onGetData((result: any) => {
            console.log("回调了：" + "x: " + result.x);
        });
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="185">参数（SensorAttr）</th><th width="365">说明</th><th width="95">类型</th><th>备注</th></tr></thead><tbody><tr><td>sensorType</td><td>传感器类型：TYPE_ALL、TYPE_GRAVITY、TYPE_ORIENTATION等</td><td>String</td><td></td></tr><tr><td>operation</td><td>传感器操作</td><td>String[]</td><td>可选</td></tr><tr><td>updateInterval</td><td>传感器采样频率</td><td>Number</td><td>可选</td></tr></tbody></table>

<table><thead><tr><th width="197">参数（LocationAttr）</th><th width="356">说明</th><th width="93.33333333333331">类型</th><th>备注</th></tr></thead><tbody><tr><td>locationType</td><td>定位方式：GPS、WiFi、5G等</td><td>String</td><td></td></tr><tr><td>operation</td><td>定位操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="482">抽象动作（SensorAction）</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用传感器的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>传感器开启监听时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>传感器原始数据流</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>传感器获取当前数据</td></tr><tr><td>onAccuracyChanged?(callback: (sensor: string, accuracy: number) => void): void</td><td>传感器精度变化时回调</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>传感器关闭时的回调</td></tr></tbody></table>

<table><thead><tr><th width="483">抽象动作（LocationAction）</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>
