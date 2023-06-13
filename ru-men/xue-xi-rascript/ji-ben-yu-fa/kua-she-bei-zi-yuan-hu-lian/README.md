# 跨设备资源互联

跨设备资源互联依托于以APP或Activity等为原子单位的应用多设备交互，如鸿蒙系统的跨设备流转（[https://developer.harmonyos.com/cn/docs/documentation/doc-guides/hop-overview-0000001092995092](https://developer.harmonyos.com/cn/docs/documentation/doc-guides/hop-overview-0000001092995092)）、Android的Cross device（[https://developer.android.com/guide/topics/connectivity/cross-device-sdk/overview](https://developer.android.com/guide/topics/connectivity/cross-device-sdk/overview)）。

在应用发起跨设备交互时，系统层管理类会回调相应的状态函数，在这些回调中进而执行资源的跨设备交互。资源的跨设备交互分为跨设备资源互补和跨设备资源协同。根据状态码区分不同类型数据发送和接收。如DEVICE\_DATA（设备数据回传）；DEVICE\_CONTROL（设备操控指令回传）。
