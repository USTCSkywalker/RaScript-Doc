# CPU开发指导

#### 示例代码（RaScript开发范式）

{% code lineNumbers="true" %}
```javascript
// 获取设备的相关信息
@Scenarios
function getDeviceInfo() {
  Device().deviceType('local').operate('get_curdata').onGetData(function (result) {
    console.log("设备信息：" + result.deviceBrand + " " + result.deviceModel
      + " 系统版本：" + result.systemName + " " + result.systemVersion);
  });
}

// 获取电池的相关信息
function getBatteryInfo() {
  Device().deviceType('local').operate('get_curdata').onGetData(function (result) {
    console.log("当前电量：" + result.battery * 100 + "%" 
      + " 正在充电：" + result.charging);
  });
}

// 斐波那契数计算
@Scenarios
function fibonacci() {
  Device().deviceType('local').operate('get_curdata').taskType("CPU_INTENSIVE").
    task(getFibonncci).onGetData(function (result) {
      console.log("计算结果为：" + result);
    });
}
```
{% endcode %}

#### 编译后TypeScript代码

{% code lineNumbers="true" %}
```typescript
// 获取设备的相关信息
function getDeviceInfo() {
  Device.getInstance().deviceType('local').operate(['get_curdata']).onGetData(function (result) {
    console.log("设备信息: " + result.deviceBrand + " " + result.deviceModel
      + " 系统版本：" + result.systemName + " " + result.systemVersion);
  }).build();
}

// 获取电池的相关信息
function getBatteryInfo() {
  Device.getInstance().deviceType('local').operate(['get_curdata']).onGetData(function (result) {
    console.log("当前电量：" + result.battery * 100 + "%" 
      + " 正在充电：" + result.charging);
  }).build();
}

// CPU性能监控
function cpuListenerStart() {
  cpuListener();
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="159">参数</th><th width="190">说明</th><th width="301">类型</th><th>备注</th></tr></thead><tbody><tr><td>deviceType</td><td>设备管理类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>CPU捕获操作</td><td>String[]</td><td>可选</td></tr><tr><td>taskType</td><td>待执行任务的类型</td><td>String</td><td>可选</td></tr><tr><td>task</td><td>待执行任务</td><td>Object</td><td>可选</td></tr><tr><td>threadPool</td><td>线程池中线程数量</td><td>Int</td><td>可选</td></tr><tr><td>execution</td><td>任务执行方式</td><td>'Async' | 'Sync'</td><td></td></tr><tr><td>powerMode</td><td>CPU性能模式</td><td>'Performance' | 'Balance' | 'Efficiency'</td><td></td></tr><tr><td>id</td><td>线程ID</td><td>Long</td><td>可选</td></tr><tr><td>name</td><td>线程名称</td><td>String</td><td>可选</td></tr><tr><td>priority</td><td>线程优先级</td><td>Int</td><td>可选</td></tr><tr><td>state</td><td>线程状态</td><td>Enum&#x3C;></td><td>可选</td></tr><tr><td>elapsedCpuTime</td><td>进程已运行时间</td><td>Long</td><td>可选</td></tr><tr><td>thermalStatus</td><td>设备当前的发热状态</td><td>'THERMAL_STATUS_NONE' | 'THERMAL_STATUS_LIGHT' | 'THERMAL_STATUS_MODERATE' | 'THERMAL_STATUS_SEVERE' | 'THERMAL_STATUS_CRITICAL' | 'THERMAL_STATUS_EMERGENCY' | 'THERMAL_STATUS_SHUTDOWN'</td><td>可选</td></tr><tr><td>isPowerSaveMode</td><td>设备当前是否处于省电模式</td><td>Boolean</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onRun</td><td>任务执行的回调</td></tr><tr><td>onThreadList</td><td>返回可用线程列表</td></tr><tr><td>onCreate</td><td>创建线程的回调</td></tr><tr><td>onDestroy</td><td>销毁线程的回调</td></tr><tr><td>onSleep</td><td>休眠线程的回调</td></tr><tr><td>onGetPriority</td><td>获取线程优先级</td></tr><tr><td>onGetState</td><td>获取线程状态</td></tr><tr><td>onGetCurrentThermalStatus</td><td>获取设备当前的发热状态</td></tr><tr><td>onGetElapsedCpuTime</td><td>获取进程已运行时间</td></tr><tr><td>onGetPoolSize</td><td>获取线程池中当前的线程数量</td></tr></tbody></table>
