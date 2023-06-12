# 传感器开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
SensorAttr {
    sensorId : Number,    // 传感器类型：TYPE_ALL、TYPE_GRAVITY、TYPE_ORIENTATION等
    delay ?: Number,    // 传感器采样频率（延迟）
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    //所有可用传感器的列表回调
onOpen ? : (result: String)=>void    // sensor开启监听时的回调
onOriginData ? : (result : any)=>void    // sensor原始数据流
onAccuracyChanged ? : (sensor: Sensor, accuracy: Number)    // sensor精度变化时回调
onClose ? : (result: String)=>void    // sensor取消监听时的回调
```
{% endcode %}
