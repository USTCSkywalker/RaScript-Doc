# 相机开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
import { Cameras } from './ResManager/CameraManager/CameraManager.ts';
import { Camera, CameraDevice } from 'react-native-vision-camera';

function App(): JSX.Element {
    const [device, setDevice] = useState<CameraDevice>();
    const camera = useRef<Camera>(null);
    
    function preview() {
        Cameras.getInstance().attr({camType:"back", operation:["preview"]}).onOpen((value) => {
            setDevice(value);
        }).build();
    }
    
    function takePhoto() {
        Cameras.getInstance().operate(['takePhoto']).setCamObj(camera.current).flash('off').qualityPrioritization('speed').skipMetadata(true).onPhoto((value) => {
            console.log("photo path:" + value);
        }).build();
    }
    
    function cameraRecording() {
        Cameras.getInstance().operate(['startRecording']).setCamObj(camera.current).build();
    }
    
    function stopCamRecording() {
        Cameras.getInstance().operate(['stopRecording']).setCamObj(camera.current).onRecordingFinished((result: any) => {
            console.log("recording path:" + result.path);
        }).build();
    }
    
    function closeCamera() {
        Cameras.getInstance().operate(['stop']).onStop((result: any) => {
            setDevice(undefined);
        }).build();
    }
  
    return (
        <SafeAreaView style={backgroundStyle}>
            <Button onPress={() => { preview(); }}
                title={"打开相机"}
            />
            {device ? (<Camera
                ref={camera}
                style={StyleSheet.absoluteFill}
                device={device}
                isActive={true}
                photo={true}
                video={true}
            />) : null
            }
            <Button onPress={() => { takePhoto(); }}
                title={"拍照"}
            />
            <Button onPress={() => { closeCamera(); }}
                title={"关闭相机"}
            />
            <Button onPress={() => { cameraRecording(); }}
                title={"开始录像"}
            />
            <Button onPress={() => { stopCamRecording(); }}
                title={"关闭录像"}
            />
        </SafeAreaView>
    );
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="194">参数</th><th width="323">说明</th><th width="133">类型</th><th>备注</th></tr></thead><tbody><tr><td>camType</td><td>相机类型：ALL、前置、后置、红外等</td><td>String</td><td></td></tr><tr><td>operation</td><td>相机操作</td><td>String[]</td><td>可选</td></tr><tr><td>photoCodec</td><td>图片编解码器</td><td>String</td><td>可选</td></tr><tr><td>qualityPrioritization</td><td>质量优先级：质量档、平衡档或速度档</td><td>'quality' | 'balanced' | 'speed'</td><td>可选</td></tr><tr><td>flash</td><td>开启或关闭闪光灯，或使用自动设置</td><td>'on' | 'off' | 'auto'</td><td>可选</td></tr><tr><td>quality</td><td>指定JPEG的质量（0-100，其中100表示最佳质量（无压缩）</td><td>Number</td><td>可选</td></tr><tr><td>enableAutoRedEyeReduction</td><td>是否开启去除红眼功能</td><td>Boolean</td><td>可选</td></tr><tr><td>skipMetadata</td><td>是否跳过原始数据的读取与映射，跳过时拍照速度更快</td><td>Boolean</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="484">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onDeviceList?(callback: (result: string[]) => void): void</td><td>所有可用相机的列表回调</td></tr><tr><td>onOpen?(callback: (result: any) => void): void</td><td>相机打开时的回调</td></tr><tr><td>onOriginData?(callback: (result: any) => void): void</td><td>相机原始数据流</td></tr><tr><td>onGetData?(callback: (result: any) => void): void</td><td>相机获取当前数据</td></tr><tr><td>onPhoto?(callback: (result: any) => void): void</td><td>相机捕获照片的回调</td></tr><tr><td>onRecordingFinished?(callback: (result: any) => void): void</td><td>相机停止录像的回调</td></tr><tr><td>onStop?(callback: (result: any) => void): void</td><td>相机关闭时的回调</td></tr></tbody></table>
