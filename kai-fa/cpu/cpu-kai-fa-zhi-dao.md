# CPU开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
CPUAttr {
    actionId : Number,    // CPU管理类型：开启捕获、关闭捕获等
    captureDelay ? : Number,    // 多久捕获⼀次
    filePaht ? : String,    // CPU信息导出路径
    filter ? : List<Number>,    // 捕获信息的类型
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用监控的CPU信息列表回调
onOpen ? : (result: String)=>void    // CPU监控开启时的回调
onOriginData ? : (result : any)=>void    // CPU监控捕获的原始数据流
onClose ? : (result: String)=>void    // CPU监控关闭时的回调
```
{% endcode %}
