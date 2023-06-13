# 跨设备资源协同

多设备可以进行资源的互补，比如在两个设备互联时，手机B可以操作手机A的摄像头行跨设备的资源协同，增强手机A的功能支持。

{% code lineNumbers="true" %}
```typescript
Cameras().regitser().operate(['takePhoto']).setCamObj(camera.current).flash('off').qualityPrioritization('speed').skipMetadata(true)
.onPhoto((value) => {
    console.log("本地相机拍摄 photo:" + value);
})
.onGetRemote((code: int, data: any, reply: any) => {
    if(code == DEVICE_CONTROL) {
        Cameras().operate(data)
    }
})
.onSetRemote(() => {
    return {code: DEVICE_CONTROL, data: ['close'], reply: new reply()}
});
```
{% endcode %}
