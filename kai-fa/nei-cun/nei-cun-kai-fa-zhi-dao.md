# 内存开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { memListenerBuild } from './ResManager/MemManager/MemManager.js';

function App(): JSX.Element {
    function memListenerStart() {
        var memory = {
            attr: { 
            },
            action: {
                onData: function (value) { console.log(value); }
            }
        };
        memListenerBuild(memory.attr, memory.action);
    }
    
    return (
        <SafeAreaView style={backgroundStyle}>
            <Button onPress={() => { memListenerStart(); }}
                title={"开启内存监测"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="147">参数</th><th width="412">说明</th><th width="90">类型</th><th>备注</th></tr></thead><tbody><tr><td>memoryType</td><td>内存管理类型：开启捕获、关闭捕获等</td><td>String</td><td></td></tr><tr><td>operation</td><td>内存捕获操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>
