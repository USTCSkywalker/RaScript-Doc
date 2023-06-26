# 跨设备资源互补

多设备可以进行资源的互补，比如手机A摄像头不能用，手机B的可以用，则在两个设备互联时，可以进行跨设备的资源互补，如手机A的应用可以收到手机B的相机回传的数据，进而增强手机A的功能支持。

{% code lineNumbers="true" %}
```typescript
// A手机此时是CamerasHost即相机主模式，camType为auto；
// 当本机有相机时，用本机设备拍照，调用onPhoto回调获取数据；
// 若本机无相机，则用附近从设备拍照，调用onGetRemote回调获取数据；
@Scenarios(CamerasHost)
function takePhoto() {
    Cameras().regitser().camType('auto').operate(['takePhoto'])
        .onPhoto((value) => {
            console.log("本地相机拍摄 photo:" + value);
        })
        .onGetRemote((code: int, data: any, reply: any) => {
            if (code == DEVICE_DATA) {
                console.log("互联设备相机拍摄 photo:" + data);
            }
        });
}
```
{% endcode %}
