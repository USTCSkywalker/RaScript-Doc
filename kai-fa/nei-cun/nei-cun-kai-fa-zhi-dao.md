# 内存开发指导

#### 静态属性

<table><thead><tr><th width="149">参数</th><th width="359">说明</th><th width="142">类型</th><th>备注</th></tr></thead><tbody><tr><td>actionId</td><td>内存管理类型：开启捕获、关闭捕获等</td><td>Number</td><td></td></tr><tr><td>captureDelay</td><td>多久捕获一次</td><td>Number</td><td>可选</td></tr><tr><td>filePath</td><td>内存信息导出路径</td><td>String</td><td>可选</td></tr><tr><td>filter</td><td>捕获信息的类型</td><td>List&#x3C;Number></td><td>可选</td></tr></tbody></table>

#### 抽象动作

| 抽象动作                                        | 说明              |
| ------------------------------------------- | --------------- |
| onDeviceList ? : (result: List\<T>) => void | 所有可用监控的内存信息列表回调 |
| onOpen ? : (result: String) => void         | 内存监控开启时的回调      |
| onOriginData ? : (result : any) => void     | 内存监控捕获的原始数据流    |
| onClose ? : (result: String) => void        | 内存监控关闭时的回调      |
| onGC ? : (result: String) => void           | GC回调            |
