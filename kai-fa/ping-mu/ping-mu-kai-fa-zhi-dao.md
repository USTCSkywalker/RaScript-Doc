# 屏幕开发指导

#### 屏幕示例代码

{% code lineNumbers="true" %}
```typescript
import { Screen } from './ResManager/ScreenManager/ScreenManager.ts';
import Video from 'react-native-video';

function App(): JSX.Element {
    const [uri, setUri] = useState<string>('');

    function screenStart() {
        // 链式设置静态属性和回调函数
        Screen.getInstance().attr({ mic: false, fps: 30, bitrate: 1024000 }).operate(["start"]).build();
    }

    function screenStop() {
        Screen.getInstance().operate(["stop", "get_curdata"]).onGetData(function (result) {
            console.log("回调了：" + "uri: " + result);
            setUri(result);
        }).build();
    }
  
    return (
        <SafeAreaView style={backgroundStyle}>
            {uri ? (
                <View style={styles.preview}>
                    <Video source={{ uri, }}
                        style={styles.video}
                    />
                </View>
            ) : null}
            <Button onPress={() => { screenStart(); }}
                title={"开始录屏"}
            />
            <Button onPress={() => { screenStop(); }}
                title={"停止录屏"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="121">参数</th><th width="435">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>fps</td><td>屏幕录制帧率</td><td>Number</td><td>可选</td></tr><tr><td>bitrate</td><td>屏幕录制比特率</td><td>Number</td><td>可选</td></tr><tr><td>mic</td><td>录屏时是否开启麦克风</td><td>Boolean</td><td>可选</td></tr><tr><td>operation</td><td>屏幕操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onStart?(callback: (result: any) => void): void</td><td>屏幕开启录制</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onStop?(callback: () => object): void</td><td>屏幕停止录制</td></tr></tbody></table>
