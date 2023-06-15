# 扬声器开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { SpeakerBuild } from './ResManager/SoundManager/SoundManager.js';

function App(): JSX.Element {
    function SpeakerPlay() {
        var speaker_play = {
            attr: {
                'SpeakerID': "common",
                'SpeakerPath': "local",
                'SpeakerTask': "play",
            },
            action: {
                onMiCList: function (result) { console.log("onMiCList:" + result); },
                onPlay: function (result) { console.log("onPlay:" + result); },
                onData: function (result) { console.log("onData:" + result); },
                onStop: function (result) { console.log("onStop:" + result); }
            }
        };
        SpeakerBuild(speaker_play.attr, speaker_play.action);
    }

    function SpeakerStop() {
        var speaker_stop = {
            attr: {
                'SpeakerID': "common",
                'SpeakerPath': "local",
                'SpeakerTask': "stop",
            },
            action: {
                onMiCList: function (result) { console.log("onMiCList:" + result); },
                onPlay: function (result) { console.log("onPlay:" + result); },
                onData: function (result) { console.log("onData:" + result); },
                onStop: function (result) { console.log("onStop:" + result); }
            }
        };
        SpeakerBuild(speaker_stop.attr, speaker_stop.action);
    }
  
    return (
        <SafeAreaView style={backgroundStyle}>
            <Button onPress={() => { SpeakerStop(); }}
                title={"speaker_stop"}
            />
            <Button onPress={() => { SpeakerPlay(); }}
                title={"speaker_play"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="135">参数</th><th width="417">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>speakerId</td><td>扬声器类型：内置、耳机、蓝牙等：TYPE_BUILTIN_SPEAKER、TYPE_BUILTIN_SPEAKER_SAFE、TYPE_BUILTIN_EARPIECE等</td><td>Number</td><td></td></tr><tr><td>sourcePath</td><td>音频源：本地，网络，Uri等</td><td>String</td><td></td></tr></tbody></table>

#### 抽象动作

| 抽象动作                                        | 说明              |
| ------------------------------------------- | --------------- |
| onDeviceList ? : (result: List\<T>) => void | 所有可用扬声器的列表回调    |
| onOpen ? : (result: String) => void         | 扬声器开启时的回调       |
| onOriginData ? : (result : any) => void     | 扬声器正在播放的音频原始数据流 |
| onClose ? : (result: String) => void        | 扬声器关闭时的回调       |
