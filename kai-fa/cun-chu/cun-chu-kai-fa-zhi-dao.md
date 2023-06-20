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

<table><thead><tr><th width="192">参数（StorageAttr）</th><th width="364">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>storageType</td><td>存储类型：DB、文件、SP</td><td>String</td><td></td></tr><tr><td>operation</td><td>操作类型：增、删、改、查</td><td>String[]</td><td>可选</td></tr><tr><td>dbPath</td><td>存储路径：以Uri的方式描述DB路径</td><td>String</td><td></td></tr><tr><td>schema</td><td>数据库Schema</td><td>any[]</td><td>可选</td></tr><tr><td>schemaVersion</td><td>数据库Schema版本</td><td>Number</td><td></td></tr><tr><td>name</td><td>存储命名</td><td>String</td><td>可选</td></tr></tbody></table>

<table><thead><tr><th width="193">参数（FileAttr）</th><th width="364">说明</th><th width="93">类型</th><th>备注</th></tr></thead><tbody><tr><td>fileType</td><td>文件类型</td><td>String</td><td></td></tr><tr><td>filename</td><td>文件名</td><td>String</td><td></td></tr><tr><td>operation</td><td>文件操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="424">抽象动作（StorageAction）</th><th>说明</th></tr></thead><tbody><tr><td>onCreate?(callback: (result: any) => void): void</td><td>DB创建回调</td></tr><tr><td>onInsert?(callback: () => object): void</td><td>DB数据插入回调</td></tr><tr><td>onSuccess?(callback: (result: any) => object): void</td><td>操作成功回调</td></tr><tr><td>onFail?(callback: (result: any) => object): void</td><td>操作失败回调</td></tr></tbody></table>

<table><thead><tr><th width="425">抽象动作（FileAction）</th><th>说明</th></tr></thead><tbody><tr><td>onCreate?(callback: () => void): void</td><td>文件创建回调</td></tr><tr><td>onRead?(callback: () => void): void</td><td>文件读取回调</td></tr><tr><td>onWrite?(callback: () => string): void</td><td>文件写入回调</td></tr><tr><td>onDelete?(callback: () => void): void</td><td>文件删除回调</td></tr><tr><td>onSuccess?(callback: () => object): void</td><td>操作成功回调</td></tr><tr><td>onFail?(callback: () => object): void</td><td>操作失败回调</td></tr></tbody></table>
