---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 屏幕开发指导

#### 屏幕示例代码（RaScript开发范式）

{% code lineNumbers="true" %}
```javascript
// 开始录屏
@Scenarios
function screenStart() {
  Screen({ mic: false, fps: 30, bitrate: 1024000 }).operate("start");
}

// 停止录屏，获取数据
@Scenarios
function screenStop() {
  Screen().operate(["stop", "get_curdata"]).onGetData(function (result) {
    console.log("回调了：" + "uri: " + result);
    setUri(result);
    displaypath = result;
  });
}

// 将要显示的内容输出到主屏
@Scenarios
function screenShow() {
  Screen().operate(["create"]).disType("front").content(UI);
}
```
{% endcode %}

#### 编译后TypeScript代码

{% code lineNumbers="true" %}
```typescript
// 开始录屏
function screenStart_default() { 
  // 设置静态属性1.{},2.链式逐个设置
  Screen.getInstance().attr({ 
    mic: false, fps: 30, bitrate: 1024000 
  }).operate(["start"]).build(); 
}
  
// 停止录屏，获取数据
function screenStop_default() { 
  Screen.getInstance().operate(["stop", "get_curdata"]).onGetData(function (result) {
    console.log("回调了：" + "uri: " + result);
    setUri(result);
    displaypath = result;
  }).build(); 
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="130">参数</th><th width="250">说明</th><th width="263">类型</th><th>备注</th></tr></thead><tbody><tr><td>fps</td><td>屏幕录制帧率</td><td>Number</td><td>可选</td></tr><tr><td>bitrate</td><td>屏幕录制比特率</td><td>Number</td><td>可选</td></tr><tr><td>mic</td><td>录屏时是否开启麦克风</td><td>Boolean</td><td>可选</td></tr><tr><td>operation</td><td>屏幕操作</td><td>String[]</td><td>可选</td></tr><tr><td>disType</td><td>屏幕类别</td><td>String</td><td>可选</td></tr><tr><td>content</td><td>屏幕显示的内容</td><td>Object</td><td>可选</td></tr><tr><td>state</td><td>屏幕状态</td><td>'STATE_OFF' | 'STATE_ON' | 'STATE_DOZE' | 'STATE_DOZE_SUSPEND' | 'STATE_ON_SUSPEND' | 'STATE_UNKNOWN'</td><td></td></tr><tr><td>orientation</td><td>屏幕显示方向</td><td>'ROTATION_0' | 'ROTATION_90' | 'ROTATION_180' | 'ROTATION_270'</td><td></td></tr><tr><td>refreshRate</td><td>屏幕刷新率</td><td>Float</td><td>可选</td></tr><tr><td>supportedHdrTypes</td><td>屏幕支持的HDR模式</td><td>'HDR_TYPE_INVALID' | 'HDR_TYPE_DOLBY_VISION' | 'HDR_TYPE_HDR10' | 'HDR_TYPE_HLG' | 'HDR_TYPE_HDR10_PLUS'</td><td></td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onStart?(callback: (result: any) => void): void</td><td>屏幕开启录制</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onStop?(callback: () => object): void</td><td>屏幕停止录制</td></tr><tr><td>onCreate?(callback: (result: any) => void): void</td><td>初始化函数</td></tr><tr><td>onResume?(callback: (result: any) => void): void</td><td>恢复函数</td></tr><tr><td>onPause?(callback: (result: any) => void): void</td><td>暂停函数</td></tr><tr><td>onDestroy?(callback: (result: any) => void): void</td><td>销毁函数</td></tr></tbody></table>
