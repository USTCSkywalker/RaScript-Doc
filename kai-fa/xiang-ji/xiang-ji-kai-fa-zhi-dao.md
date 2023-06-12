# 相机开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
CameraAttr {
    cameraId : String,    // 相机类型：ALL、前置、后置、红外等
    cameraMode : Number,     // 相机模式：PREVIEW、PHOTO、VIDEO、SNAPSHOT、STOP_PREVIEW、STOP_VIDEO、CLOSE
    photoMode ？: Number,    // 拍照次数：0（单拍）、（>0）连拍次数
    photoFormat ? : String,    // 照⽚格式：Bitmap、JPEG、PNG
    photoPath ? : String,    // 照⽚存储路径
    focusMode ? : Number,    // 相机对焦⽅式：⾃动对焦、固定对焦、微距对焦或⽆限远对焦
    sceneMode ? : Number,    // 对特定类型的摄影场景（例如夜景、海滩场景、雪景或烛光场景）应⽤预设模式
    flashMode ? : Number,    // 开启或关闭闪光灯，或使⽤⾃动设置
    whiteBalance ? : Boolean,    // 开启或关闭⽩平衡设置
    videoFormat ? : String,    // 视频格式：
    videoPath ? : String,    // 视频存储路径
    timeFormat ? : String,    // 照⽚或video携带时间信息
    locationFormat ? : String,    // 照⽚或video携带位置信息
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用相机的列表回调
onOpen ? : (result: String)=>void    // 相机打开时的回调
onOriginData ? : (result : any)=>void    // 相机原始数据流
onPreview ? : (result: CameraFrame)=>void    // 相机预览回调
onPhoto ? : (result: Bitmap)=>void    // 相机捕获照片的回调
onVideo ? : (result: CameraFrame)=>void    // 相机录像的回调
onStopPreview ? : (result: String)=>void    // 相机停止预览的回调
onStopVideo ? : (result: String)=>void    // 相机停止录像的回调
onClose ? : (result: String)=>void    // 相机关闭时的回调
```
{% endcode %}
