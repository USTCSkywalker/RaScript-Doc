# 扬声器开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
SpeakerAttr {
    speakerId : Number,    // 扬声器类型：内置、耳机、蓝牙等：TYPE_BUILTIN_SPEAKER、TYPE_BUILTIN_SPEAKER_SAFE、TYPE_BUILTIN_EARPIECE等
    sourcePath : String,    // 音频源：本地，⽹络，Uri等
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用扬声器的列表回调
onOpen ? : (result: String)=>void    // 扬声器开启时的回调
onOriginData ? : (result : any)=>void    // 扬声器正在播放的音频原始数据流
onClose ? : (result: String)=>void    // 扬声器关闭时的回调
```
{% endcode %}
