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

<table><thead><tr><th width="135">参数</th><th width="425">说明</th><th width="90">类型</th><th>备注</th></tr></thead><tbody><tr><td>deviceType</td><td>设备管理类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>CPU捕获操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>
