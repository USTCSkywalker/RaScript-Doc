# 麦克风开发指导

#### 静态属性

<table><thead><tr><th width="151">参数</th><th width="404">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>micId</td><td>麦克风类型：普通、降噪、USB外接</td><td>Number</td><td></td></tr><tr><td>outputFormat</td><td>音频格式</td><td>String</td><td>可选</td></tr><tr><td>outputPath</td><td>音频存放路径</td><td>String</td><td>可选</td></tr><tr><td>encoderId</td><td>音频编码器类型</td><td>Number</td><td>可选</td></tr></tbody></table>

#### 抽象动作

| 抽象动作                                        | 说明           |
| ------------------------------------------- | ------------ |
| onDeviceList ? : (result: List\<T>) => void | 所有可用Mic的列表回调 |
| onOpen ? : (result: String) => void         | Mic开启时的回调    |
| onOriginData ? : (result : any) => void     | Mic录制的原始数据流  |
| onClose ? : (result: String) => void        | Mic关闭时的回调    |
