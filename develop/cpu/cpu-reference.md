# CPU开发指导

#### 示例代码（RaScript开发范式）

{% code lineNumbers="true" %}
```javascript
// 创建线程
@Scenarios
function createThread() {
  vCPU().id(1).name('testThread').priority(3).onCreate(function() {
    console.log("线程创建成功");
  });
}

// 利用线程池执行网络爬虫任务
@Scenarios
function crawlerPool() {
  vCPU().threadPool(5).powerMode('Balance').task(webCrawler).execMode('Async')
  .onRun(function (result) {
    console.log(result);
  });
}

// 获取设备的相关信息
@Scenarios
function getDeviceInfo() {
  Device().deviceType('local').operate('get_curdata').onGetData(function (result) {
    console.log("设备信息：" + result.deviceBrand + " " + result.deviceModel
      + " 系统版本：" + result.systemName + " " + result.systemVersion);
  });
}

// 获取电池的相关信息
@Scenarios
function getBatteryInfo() {
  Device().deviceType('local').operate('get_curdata').onGetData(function (result) {
    console.log("当前电量：" + result.battery * 100 + "%" 
      + " 正在充电：" + result.charging);
  });
}

// 斐波那契数计算
@Scenarios
function fibonacci() {
  vCPU().deviceType('local').operate('get_curdata').taskType("CPU_INTENSIVE").
    task(getFibonacci).onGetData(function (result) {
      console.log("计算结果为：" + result);
    });
}
```
{% endcode %}

#### 编译后TypeScript代码

{% code lineNumbers="true" %}
```typescript
// 创建线程
function createThread() {
  vCPU.getInstance().id(1).name('testThread').priority(3).onCreate(function() {
    console.log("线程创建成功");
  }).build();
}

// 利用线程池执行网络爬虫任务
function crawlerPool() {
  vCPU.getInstance().threadPool(5).powerMode('Balance').task(webCrawler).execMode('Async')
  .onRun(function (result) {
    console.log(result);
  }).build();
}

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

<table><thead><tr><th width="159">参数</th><th width="224">说明</th><th width="264">类型</th><th>备注</th></tr></thead><tbody><tr><td>deviceType</td><td>设备管理类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>CPU捕获操作</td><td>String[]</td><td>可选</td></tr><tr><td>taskType</td><td>待执行任务的类型</td><td>String</td><td>可选</td></tr><tr><td>task</td><td>待执行任务</td><td>Object</td><td>可选</td></tr><tr><td>threadPool</td><td>线程池中线程数量</td><td>Int</td><td>可选</td></tr><tr><td>execMode</td><td>任务执行方式</td><td>'Async' | 'Sync'</td><td></td></tr><tr><td>powerMode</td><td>CPU性能模式</td><td>'Performance' | 'Balance' | 'Efficiency' | 'PowerSaving'</td><td></td></tr><tr><td>id</td><td>线程ID</td><td>Long</td><td>可选</td></tr><tr><td>name</td><td>线程名称</td><td>String</td><td>可选</td></tr><tr><td>priority</td><td>线程优先级</td><td>Int</td><td>可选</td></tr><tr><td>state</td><td>线程状态</td><td>Enum&#x3C;></td><td>可选</td></tr><tr><td>sleeptime</td><td>线程休眠时长</td><td>Long</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="505">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onRun?(callback: (result: any) => void): void</td><td>任务执行的回调</td></tr><tr><td>onThreadList?(callback: (result: string[]) => void): void</td><td>返回可用线程列表</td></tr><tr><td>onCreate?(callback: (result: any) => void): void</td><td>创建线程的回调</td></tr><tr><td>onDestroy?(callback: (result: any) => void): void</td><td>销毁线程的回调</td></tr><tr><td>onSleep?(callback: (result: any) => void): void</td><td>使当前正在执行的线程休眠（暂时停止执行）指定的毫秒数</td></tr><tr><td>onSetPriority?(callback: (newPriority: int) => void): void</td><td>更改线程的优先级，线程的优先级将设置为指定的priority和该线程的线程组允许的最大优先级中的较小值</td></tr><tr><td>onGetPriority?(callback: (threadPriority: int) => void): void</td><td>获取线程优先级</td></tr><tr><td>onGetState?(callback: (threadState: any) => void): void</td><td>获取线程状态</td></tr><tr><td>onGetPoolSize?(callback: (result: int) => void): void</td><td>获取当前线程池中的线程数量</td></tr><tr><td>onGetCurrentThermalStatus?(callback: (result: any) => void): void</td><td>获取设备当前的发热状态</td></tr><tr><td>onGetElapsedCpuTime?(callback: (result: long) => void): void</td><td>获取进程已运行时间</td></tr><tr><td>onGetPowerMode?(callback: (result: any) => void): void</td><td>获取当前CPU性能模式</td></tr></tbody></table>