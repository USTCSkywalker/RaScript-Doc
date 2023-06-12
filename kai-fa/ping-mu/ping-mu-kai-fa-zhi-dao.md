# 屏幕开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
displayAttr {
    displayId : Number,    // 屏幕类型：前屏、后屏等
    displayMode : Number,    // 屏幕操作类型：显示、共享、录制、锁定、唤醒
    shareDisplay ? : Number,    // 屏幕共享类型：屏幕共享、区域共享、窗口共享
    brightness ? : Number,    // 屏幕亮度
    orientation ? : Number,    // 屏幕方向
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用屏幕列表回调
onOpen ? : (result: String)=>void    // 屏幕开启监听时的回调
onOriginData ? : (result : any)=>void    // 屏幕采集原始数据流
onStartShare ? : (result: String)=>void    // 屏幕开启共享
onStopShare ? : (result: String)=>void    // 屏幕停止共享
onStartMark ? : (result: String)=>void    // 屏幕开启标注
onStopMark ? : (result: String)=>void    // 屏幕停止标注
onStartRecording ? : (result: String)=>void    // 屏幕开启录制
onStopRecording ? : (result: String)=>void    // 屏幕停止录制
onClose ? : (result: String)=>void    // 屏幕关闭时的回调
```
{% endcode %}
