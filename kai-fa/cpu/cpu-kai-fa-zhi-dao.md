# CPU开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
@Scenarios
function getDeviceInfo() {
    Device().deviceType('local').operate('get_curdata').onGetData(function (result) {
      console.log("设备信息: " + result.deviceBrand + " " + result.deviceModel
        + " - " + result.systemName + " " + result.systemVersion + " 当前电量: " + result.battery * 100 + "%");
    });
  }
  /斐波那契数计算
@Scenarios
function fibonacci() {
Device().deviceType('local').operate('get_curdata').taskType("CPU_INTENSIVE").
task(getFibonncci).onGetData(function (result) {
      console.log("计算结果为: " + result);
    });
}

```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="135">参数</th><th width="425">说明</th><th width="90">类型</th><th>备注</th></tr></thead><tbody><tr><td>deviceType</td><td>设备管理类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>CPU捕获操作</td><td>String[]</td><td>可选</td></tr><tr><td>taskType</td><td>待执行任务的类型</td><td>String</td><td>可选</td></tr><tr><td>task</td><td>待执行任务</td><td>object</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>
