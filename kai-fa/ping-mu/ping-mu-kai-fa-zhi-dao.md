# 屏幕开发指导

#### 静态属性

<table><thead><tr><th width="145">参数</th><th width="407">说明</th><th width="98">类型</th><th>备注</th></tr></thead><tbody><tr><td>displayId</td><td>屏幕类型：前屏、后屏等</td><td>Number</td><td></td></tr><tr><td>displayMode</td><td>屏幕操作类型：显示、共享、录制、锁定、唤醒</td><td>Number</td><td></td></tr><tr><td>shareDisplay</td><td>屏幕共享类型：屏幕共享、区域共享、窗口共享</td><td>Number</td><td>可选</td></tr><tr><td>brightness</td><td>屏幕亮度</td><td>Number</td><td>可选</td></tr><tr><td>orientation</td><td>屏幕方向</td><td>Number</td><td>可选</td></tr></tbody></table>

#### 抽象动作

| 抽象动作                                          | 说明         |
| --------------------------------------------- | ---------- |
| onDeviceList ? : (result: List\<T>) => void   | 所有可用屏幕列表回调 |
| onOpen ? : (result: String) => void           | 屏幕开启监听时的回调 |
| onOriginData ? : (result : any) => void       | 屏幕采集原始数据流  |
| onStartShare ? : (result: String) => void     | 屏幕开启共享     |
| onStopShare ? : (result: String) => void      | 屏幕停止共享     |
| onStartMark ? : (result: String) => void      | 屏幕开启标注     |
| onStopMark ? : (result: String) => void       | 屏幕停止标注     |
| onStartRecording ? : (result: String) => void | 屏幕开启录制     |
| onStopRecording ? : (result: String) => void  | 屏幕停止录制     |
| onClose ? : (result: String) => void          | 屏幕关闭时的回调   |
