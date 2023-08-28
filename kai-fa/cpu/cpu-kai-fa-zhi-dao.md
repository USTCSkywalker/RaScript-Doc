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

<table><thead><tr><th width="159">参数</th><th width="190">说明</th><th width="301">类型</th><th>备注</th></tr></thead><tbody><tr><td>deviceType</td><td>设备管理类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>CPU捕获操作</td><td>String[]</td><td>可选</td></tr><tr><td>taskType</td><td>待执行任务的类型</td><td>String</td><td>可选</td></tr><tr><td>task</td><td>待执行任务</td><td>object</td><td>可选</td></tr><tr><td>getId</td><td>线程ID</td><td>Long</td><td>可选</td></tr><tr><td>getPriority</td><td>线程优先级</td><td>Int</td><td>可选</td></tr><tr><td>getState</td><td>线程状态</td><td>Enum&#x3C;></td><td>可选</td></tr><tr><td>elapsedCpuTime</td><td>进程已运行时间</td><td>Long</td><td>可选</td></tr><tr><td>thermalStatus</td><td>设备当前的发热状态</td><td>'THERMAL_STATUS_NONE' | 'THERMAL_STATUS_LIGHT' | 'THERMAL_STATUS_MODERATE' | 'THERMAL_STATUS_SEVERE' | 'THERMAL_STATUS_CRITICAL' | 'THERMAL_STATUS_EMERGENCY' | 'THERMAL_STATUS_SHUTDOWN'</td><td>可选</td></tr><tr><td>isPowerSaveMode</td><td>设备当前是否处于省电模式</td><td>Boolean</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>
