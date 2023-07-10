# 相机开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
//预览
@Scenarios
function preview() {
  Cameras().camType(settingData.camType).operate("preview").onOpen((value) => {
    setDevice(value);
  });
}
//拍照：默认场景，或节能场景
@Scenarios(Default|EnergySaving)
function takePhoto() {
  Cameras().operate('takePhoto').setCamObj(camera.current).skipMetadata(true)
    .onPhoto((value) => {
      console.log("photo path:" + value);
      photopath = value;
    });
}
//参数设置：默认场景，或节能场景
@Scenarios(Default|EnergySaving)
function takePhotoSetting() {
  Cameras().setCamObj(camera.current).flash(settingData.flash)
    .qualityPrioritization(settingData.qualityPrioritization)
    .enableAutoRedEyeReduction(settingData.enableAutoRedEyeReduction)
    .operate("");
}
//录像
@Scenarios
function cameraRecording() {
  Cameras().operate('startRecording').setCamObj(camera.current);
}
//停止录像
@Scenarios
function stopCamRecording() {
  Cameras().operate('stopRecording').setCamObj(camera.current)
    .onRecordingFinished((result: any) => {
    console.log("recording path:" + result.path);
    videopath = result.path;
  });
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="194">参数</th><th width="323">说明</th><th width="133">类型</th><th>备注</th></tr></thead><tbody><tr><td>camType</td><td>相机类型：前置、后置等</td><td>String</td><td></td></tr><tr><td>operation</td><td>相机操作</td><td>String[]</td><td>可选</td></tr><tr><td>photoCodec</td><td>图片编解码器</td><td>String</td><td>可选</td></tr><tr><td>qualityPrioritization</td><td>质量优先级：质量档、平衡档或速度档</td><td>'quality' | 'balanced' | 'speed'</td><td>可选</td></tr><tr><td>flash</td><td>开启或关闭闪光灯，或使用自动设置</td><td>'on' | 'off' | 'auto'</td><td>可选</td></tr><tr><td>quality</td><td>指定JPEG的质量（0-100，其中100表示最佳质量（无压缩）</td><td>Number</td><td>可选</td></tr><tr><td>enableAutoRedEyeReduction</td><td>是否开启去除红眼功能</td><td>Boolean</td><td>可选</td></tr><tr><td>skipMetadata</td><td>是否跳过原始数据的读取与映射，跳过时拍照速度更快</td><td>Boolean</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="484">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用相机的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>相机打开时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>相机原始数据流</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>相机获取当前数据</td></tr><tr><td>onPhoto?(callback: (result: any) => void): void</td><td>相机捕获照片的回调</td></tr><tr><td>onRecordingFinished?(callback: (result: any) => void): void</td><td>相机停止录像的回调</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>相机关闭时的回调</td></tr></tbody></table>
