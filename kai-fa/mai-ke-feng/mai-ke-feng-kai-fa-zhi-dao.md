# 麦克风开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
MicAttr {
    micId : Number,    // mic类型：普通、降噪、USB外接
    outputFormat ? : String,    // 音频格式
    outputPath ? : String,    // 音频存放路径
    encoderId ? : Number,    // 音频编码器类型
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可⽤Mic的列表回调
onOpen ? : (result: String)=>void    // Mic开启时的回调
onOriginData ? : (result : any)=>void    // Mic录制的原始数据流
onClose ? : (result: String)=>void    // Mic关闭时的回调
```
{% endcode %}
