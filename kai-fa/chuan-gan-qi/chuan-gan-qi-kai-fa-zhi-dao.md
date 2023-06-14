# 传感器开发指导

#### 静态属性

<table><thead><tr><th width="114">参数</th><th width="442">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>sensorId</td><td>传感器类型：TYPE_ALL、TYPE_GRAVITY、TYPE_ORIENTATION等</td><td>Number</td><td></td></tr><tr><td>delay</td><td>传感器采样频率（延迟）</td><td>Number</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="503">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList ? : (result: List&#x3C;T>) => void</td><td>所有可用传感器的列表回调</td></tr><tr><td>onOpen ? : (result: String) => void</td><td>sensor开启监听时的回调</td></tr><tr><td>onOriginData ? : (result : any) => void</td><td>sensor原始数据流</td></tr><tr><td>onAccuracyChanged ? : (sensor: Sensor, accuracy: Number)</td><td>sensor精度变化时回调</td></tr><tr><td>onClose ? : (result: String) => void</td><td>sensor取消监听时的回调</td></tr></tbody></table>
