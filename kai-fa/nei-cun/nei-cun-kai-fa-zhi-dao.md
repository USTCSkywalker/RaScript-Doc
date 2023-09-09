# 内存开发指导

#### 示例代码（RaScript开发范式）

{% code lineNumbers="true" %}
```javascript
// 获取内存使用情况并计算当前内存利用率
@Scenarios
function getMemoryInfo() {
  Memory().memoryType('local').operate('get_curdata').onGetData(function (result) {
    console.log("内存使用情况：" + result.usedMemory.toFixed(2) + 'GB/' 
      + result.totalMemory.toFixed(2) + "GB " + "当前内存利用率：" 
      + (result.usedMemory / result.totalMemory).toFixed(2) + '%');
  });
}

// 设置变量的共享范围
@Scenarios
function setShareVar() {
  Memory().memoryType('local').operate('set_data')
  .content({name:"Jack",age:10,5:true})
  .scope(['rs1','rs2']);
}

@Scenarios
function getShareVar() {
  Memory().memoryType('local').operate('get_data')
  .content({name:null})
  .scope(['rs1']).onGetData(function (result) {
    console.log('name:',result);
  });;
}
```
{% endcode %}

#### 编译后TypeScript代码

{% code lineNumbers="true" %}
```typescript
// 获取内存使用情况并计算当前内存利用率
function getMemoryInfo() {
  Memory.getInstance().memoryType('local').operate(['get_curdata']).onGetData(function (result) {
    console.log("内存使用情况: " + result.usedMemory.toFixed(2) + 'GB/' 
      + result.totalMemory.toFixed(2) + "GB " + "当前内存利用率: " 
      + (result.usedMemory / result.totalMemory).toFixed(2) + '%');
  }).build();
}

// 内存性能监控
function memListenerStart() {
  memListener();
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="141">参数</th><th width="175">说明</th><th width="334">类型</th><th>备注</th></tr></thead><tbody><tr><td>memoryType</td><td>内存类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>内存相关操作</td><td>String[]</td><td>可选</td></tr><tr><td>scope</td><td>变量作用范围</td><td>String[]</td><td>可选</td></tr><tr><td>content</td><td>变量</td><td>Object</td><td>可选</td></tr><tr><td>name</td><td>共享内存名称</td><td>String</td><td>可选</td></tr><tr><td>size</td><td>共享内存大小</td><td>Int</td><td></td></tr><tr><td>prot</td><td>共享内存映射区域的权限</td><td>'Read' | 'Write' | 'Exec' | 'None'</td><td></td></tr><tr><td>offset</td><td>共享内存映射区域的偏移量</td><td>Int</td><td></td></tr><tr><td>length</td><td>共享内存映射区域的长度</td><td>Int</td><td></td></tr><tr><td>onTrimMemory</td><td>内存可用状态</td><td>'TRIM_MEMORY_COMPLETE' | 'TRIM_MEMORY_MODERATE' | 'TRIM_MEMORY_BACKGROUND' | 'TRIM_MEMORY_UI_HIDDEN' | 'TRIM_MEMORY_RUNNING_CRITICAL' | 'TRIM_MEMORY_RUNNING_LOW' | 'TRIM_MEMORY_RUNNING_MODERATE'</td><td>可选</td></tr><tr><td>processMemoryInfo</td><td>一个或多个进程的内存使用情况</td><td>String[]</td><td>可选</td></tr><tr><td>runningAppProcesses</td><td>设备上正在运行的应用程序进程的列表</td><td>List&#x3C;></td><td>可选</td></tr><tr><td>isLowRamDevice</td><td>设备是否为RAM低于1GB的低内存设备</td><td>Boolean</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onCreateSharedMemory</td><td></td></tr><tr><td>onGetSharedMemorySize</td><td></td></tr><tr><td>onMap</td><td></td></tr><tr><td>onUnmap</td><td></td></tr></tbody></table>

