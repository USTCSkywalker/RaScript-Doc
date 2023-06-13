# 代码多设备兼容性

同一套代码可以根据目标平台进行适配，有两种方式协作：

1.SDK层提供一致接口，在SDK层做适配；

2.语法层，根据@target(phone, pad)进行条件编译适配。

{% code lineNumbers="true" %}
```typescript
@target(phone, pad, laptop)
Cameras().operate(['takePhoto']).setCamObj(camera.current).flash('off').qualityPrioritization('speed').skipMetadata(true)
.onPhoto((value) => {
    console.log("本地相机拍摄 photo:" + value);
})；
```
{% endcode %}
