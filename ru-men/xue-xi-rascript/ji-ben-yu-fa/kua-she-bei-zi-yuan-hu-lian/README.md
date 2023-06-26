# 跨设备资源互联

跨设备资源互联依托于以APP或Activity等为原子单位的应用多设备交互，如鸿蒙系统的跨设备流转（[https://developer.harmonyos.com/cn/docs/documentation/doc-guides/hop-overview-0000001092995092](https://developer.harmonyos.com/cn/docs/documentation/doc-guides/hop-overview-0000001092995092)）、Android的Cross device（[https://developer.android.com/guide/topics/connectivity/cross-device-sdk/overview](https://developer.android.com/guide/topics/connectivity/cross-device-sdk/overview)）。

在应用发起跨设备交互时，系统层管理类会回调相应的状态函数，在这些回调中进而执行资源的跨设备交互。资源的跨设备交互分为跨设备资源互补和跨设备资源协同。根据状态码区分不同类型数据发送和接收。如DEVICE\_DATA（设备数据回传）；DEVICE\_CONTROL（设备操控指令回传）。

## 资源互联流程

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

流程图说明：

设备A和设备B有相同的APP。

以相机使用为例：调用相机资源时，可以设置camType：local(本机)，auto(自动)，remote(远端)。

图中A调用相机时，流程如下：

1.首先判断本地相机是否可用；

2.如果可用，且camType是local或auto时，直接用本地相机进行拍照。

3.如果camType为remote时，表示A需要调用远端相机，当remoteKind为control时，表示直接发送指令，使远端相机自动执行后回传数据。否则，需要人为操控远端设备，再回传数据。

如果本地相机不可用，当camType为auto或者remote时，表示调用远端设备，走上述第3步流程。否则直接提示相机不可用。
