# 存储开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { Mic } from './ResManager/MicManager/MicManager.ts';
import { Storage } from './ResManager/StorageManager/StorageManager.ts';
import { MicAttr, StorageAttr } from './ResManager/api/Attr.ts';

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

    // Scenarios有参数：Auto(自适应模式)；Call(通话模式)
    function startRecording(): void {
        Mic.getInstance().attr(new mic_start()).onOriginData(function (result) {
            console.log("回调了录音时间：" + result);
            setRecordTime(result);
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
        // 存储到DB
        // Storage.getInstance().attr({storageType:"db",operation:["create"],schema:RecordingSchema})
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

<table><thead><tr><th width="136">参数</th><th width="404">说明</th><th width="107">类型</th><th>备注</th></tr></thead><tbody><tr><td>storeId</td><td>存储类型：DB、文件、SP</td><td>Number</td><td></td></tr><tr><td>storeIdPath</td><td>存储路径：以Uri的方式描述DB路径、文件路径</td><td>String</td><td></td></tr><tr><td>actionId</td><td>操作类型：增、删、改、查</td><td>Number</td><td></td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="437">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onRfile ? : (result : any) => void</td><td>读取文件回调</td></tr><tr><td>onWfile ? : (file : File) => void</td><td>写入回调，再回调中向file写入数据</td></tr><tr><td>onOpenDB ? : (result: String) => void</td><td>DB打开回调</td></tr><tr><td>onInsterDBData ? : (result: InsterObject)) => void</td><td>DB数据插入回调</td></tr><tr><td>onUpdateDBData ? : (result: UpdateObject)) => void</td><td>DB数据更新回调</td></tr><tr><td>onDeleteDBData ? : (result: String)) => void</td><td>DB数据删除回调</td></tr><tr><td>onSelectDBData ? : (result : any) => void</td><td>DB数据选择回调</td></tr><tr><td>onCreateDBTable ? : (result: String)) => void</td><td>DB创建表回调</td></tr><tr><td>onDeleteDBTable ? : (result: String)) => void</td><td>DB删除表回调</td></tr><tr><td>onCreatDB ? : (result: String)) => void</td><td>DB创建回调</td></tr><tr><td>onDeleteDB ? : () => void</td><td>DB删除回调</td></tr><tr><td>onCloseDB ? : (result: String) => void</td><td>DB关闭回调</td></tr></tbody></table>
