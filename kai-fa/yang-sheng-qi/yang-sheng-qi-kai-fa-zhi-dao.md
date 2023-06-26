# 扬声器开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
//播放声音
@Scenarios
function startRecording() {
    Speaker().speakerType("local").audioName(str).operate(['play']);
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="135">参数</th><th width="417">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>speakType</td><td>扬声器类型：内置、耳机、蓝牙等：TYPE_BUILTIN_SPEAKER、TYPE_BUILTIN_SPEAKER_SAFE、TYPE_BUILTIN_EARPIECE等</td><td>String</td><td></td></tr><tr><td>audioName</td><td>音频源：本地，网络，Uri等</td><td>String</td><td></td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="451">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用扬声器的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>扬声器开启时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>扬声器正在播放的音频原始数据流</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>扬声器关闭时的回调</td></tr></tbody></table>
