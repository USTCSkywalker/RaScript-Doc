# 跨设备资源协同

多设备可以进行资源的互补，比如在两个设备互联时，手机A可以操作手机B的摄像头进行跨设备的资源协同，增强手机B的功能支持。

{% code lineNumbers="true" %}
```typescript
//A手机此时是相机主模式，发送指令，控制从设备进行拍照操作
@Scenarios(CamerasHost)
function takePhoto() {
    Cameras().regitser().camType('remote').operate(['takePhoto'])
        .onSetRemote(() => {
            return { code: DEVICE_CONTROL, data: curvalue, reply: new reply() }
        });
}
```
{% endcode %}

```typescript
// B手机是从模式 接收到A发送的指令后，自动触发拍照，执行下面takePhoto
// 再回传数据
@Scenarios(CamerasSlave)
function takePhoto() {
    Cameras().regitser().camType('remote').operate(['takePhoto'])
        .onSetRemote(() => {
            return { code: DEVICE_DATA, data: curvalue, reply: new reply() }
        });
}
```
