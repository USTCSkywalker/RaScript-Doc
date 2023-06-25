# 麦克风开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
@Scenarios
function startRecording() {
    //开启Mic，获取当前录音时长
    Mic(mic_start).onOriginData((result: any) => {
        console.log("回调了录音时间：" + result);
        setRecordTime(result);
    });
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="140">参数</th><th width="416">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>micType</td><td>麦克风类型：普通、降噪、USB外接</td><td>String</td><td></td></tr><tr><td>audioName</td><td>音频命名</td><td>String</td><td>可选</td></tr><tr><td>operation</td><td>麦克风操作</td><td>String[]</td><td>可选</td></tr><tr><td>encoding</td><td>音频编码格式</td><td>String</td><td>可选</td></tr><tr><td>channels</td><td>麦克风信道</td><td>Number</td><td>可选</td></tr><tr><td>sampleRate</td><td>麦克风采样率</td><td>Number</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="425">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用麦克风的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>麦克风开启时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>麦克风录制的原始数据流</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>麦克风获取当前数据</td></tr><tr><td>onPaused?(callback: (result: string) => void): void</td><td>麦克风暂停的回调</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>麦克风关闭时的回调</td></tr></tbody></table>
