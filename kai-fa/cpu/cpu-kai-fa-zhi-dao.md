# CPU开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { cpuListenerBuild } from './ResManager/CPUManager/CPUManager.js';

function App(): JSX.Element {
    function cpuListenerStart() {
        var cpu = {
            attr: { 
            },
            action: {
                onData: function (value) { console.log(value); }
            }
        };
        cpuListenerBuild(cpu.attr, cpu.action);
    }
    
    return (
        <SafeAreaView style={backgroundStyle}>
            <Button onPress={() => { cpuListenerStart(); }}
                title={"开启CPU监测"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="149">参数</th><th width="359">说明</th><th width="142">类型</th><th>备注</th></tr></thead><tbody><tr><td>actionId</td><td>CPU管理类型：开启捕获、关闭捕获等</td><td>Number</td><td></td></tr><tr><td>captureDelay</td><td>多久捕获一次</td><td>Number</td><td>可选</td></tr><tr><td>filePath</td><td>CPU信息导出路径</td><td>String</td><td>可选</td></tr><tr><td>filter</td><td>捕获信息的类型</td><td>List&#x3C;Number></td><td>可选</td></tr></tbody></table>

#### 抽象动作

| 抽象动作                                        | 说明               |
| ------------------------------------------- | ---------------- |
| onDeviceList ? : (result: List\<T>) => void | 所有可用监控的CPU信息列表回调 |
| onOpen ? : (result: String) => void         | CPU监控开启时的回调      |
| onOriginData ? : (result : any) => void     | CPU监控捕获的原始数据流    |
| onClose ? : (result: String) => void        | CPU监控关闭时的回调      |
