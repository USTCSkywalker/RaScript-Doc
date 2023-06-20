# 麦克风开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { Mic } from './ResManager/MicManager/MicManager.ts';
import { Location } from './ResManager/LocationManager/LocationManager.ts';
import { Storage } from './ResManager/StorageManager/StorageManager.ts';
import { MicAttr, LocationAttr, StorageAttr } from './ResManager/api/Attr.ts';

const RecordingSchema = [{
    name: "Recording1",
    properties: {
        path: 'string',
        position: 'string'
    }
}];

class mic_local implements MicAttr {
    micType = "local";
    encoding = "aac";
    channels = 1;
    sampleRate = 22050;
    audioName = "wm_test1.aac"
}

class mic_start extends mic_local {
    operation = ["start"];
}

class storage_insert implements StorageAttr {
    storageType = "db";
    operation = ["insert"];
    name = "Recording1";
    schema = RecordingSchema;
}

function App(): JSX.Element {
    const [recordTime, setRecordTime] = useState(0);
    const [location, setLocation] = useState({ "currentLongitude": "null", "currentLatitude": "null" });

    // Scenarios有参数：Auto(自适应模式)；Call(通话模式)
    function startRecording(): void {
        // 开启Mic，获取当前录音时长
        Mic.getInstance().attr(new mic_start()).onOriginData(function (result) {
            console.log("回调了录音时间：" + result);
            setRecordTime(result);
        }).sceAttr(new Auto(), new Call()).build();
        // 开启位置监听，获取当前位置
        Location.getInstance().operate(["continuous"]).onOriginData(function (result) {
            console.log("回调了当前位置：" + "经度：" + result.currentLongitude + "纬度：" + result.currentLatitude);
            setLocation(result);
        }).sceAttr(new Auto(), new Call()).build();
    }
    
    // Scenarios有参数：Strict(严格模式)
    function stopRecording() {
        var recodingFile = " ";
        var position1 = " ";
        // 停止录音，获取文件路径数据
        Mic.getInstance().attr(new mic_local()).operate(["stop", "get_lastdata"]).onGetData(function (result) {
            recodingFile = result;
            console.log("回调了当前录音路径：" + recodingFile);
        }).sceAttr(new Strict()).build();
        // 停止位置监听，获取最近一次位置信息
        Location.getInstance().operate(["stop", "get_lastPos"]).onGetData(function (result) {
            position1 = JSON.stringify(result);
        }).sceAttr(new Strict()).build();
        // 存储到DB
        Storage.getInstance().attr(new storage_insert()).onInsert(function () {
            console.log("回调了：插入函数");
            return {
                path: recodingFile,
                position: position1
            };
        }).sceAttr(new Strict()).build();
    }
  
    return (
        <SafeAreaView style={backgroundStyle}>
            <View style={{ width: 200, height: 40, backgroundColor: "darkcyan", margin: 5 }}>
                <Text style={{ fontSize: 16 }}>录音文件时长(S):{recordTime}</Text>
            </View>
            <View style={{ width: 200, height: 40, backgroundColor: "darkcyan", margin: 5 }}>
                <Text style={{ fontSize: 16 }}>位置:{"纬度：" + location.currentLatitude + "经度：" + location.currentLongitude}</Text>
            </View>
            <Button onPress={() => { startRecording(); }}
                title={"启动录音"}
            />
            <Button onPress={() => { stopRecording(); }}
                title={"停止录音"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="140">参数</th><th width="416">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>micType</td><td>麦克风类型：普通、降噪、USB外接</td><td>String</td><td></td></tr><tr><td>audioName</td><td>音频命名</td><td>String</td><td>可选</td></tr><tr><td>operation</td><td>麦克风操作</td><td>String[]</td><td>可选</td></tr><tr><td>encoding</td><td>音频编码格式</td><td>String</td><td>可选</td></tr><tr><td>channels</td><td>麦克风信道</td><td>Number</td><td>可选</td></tr><tr><td>sampleRate</td><td>麦克风采样率</td><td>Number</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="425">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用麦克风的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>麦克风开启时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>麦克风录制的原始数据流</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>麦克风获取当前数据</td></tr><tr><td>onPaused?(callback: (result: string) => void): void</td><td>麦克风暂停的回调</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>麦克风关闭时的回调</td></tr></tbody></table>
