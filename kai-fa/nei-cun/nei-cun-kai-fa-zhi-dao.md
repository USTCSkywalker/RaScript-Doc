# 内存开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
MemAttr {
    actionId : Number,    // 内存管理类型：GC、捕获内存信息等
    captureDelay ? : Number,    // 多久捕获⼀次
    filePath ? : String,    // 内存信息导出路径
    filter ? : List<Number>,    // 捕获信息的类型
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用监控的内存信息列表回调
onOpen ? : (result: String)=>void    // 内存监控开启时的回调
onOriginData ? : (result : any)=>void    // 内存监控捕获的原始数据流
onClose ? : (result: String)=>void    // 内存监控关闭时的回调
onGC ? : (result: String)=>void    // GC回调
```
{% endcode %}
