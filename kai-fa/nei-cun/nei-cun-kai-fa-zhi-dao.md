# 内存开发指导

#### 示例代码（RaScript开发范式）

{% code lineNumbers="true" %}
```javascript
// 创建共享内存区域
@Scenarios
function createSharedMemory() {
  Memory().name('testSharedMemory').size(256).onCreateSharedMemory(function() {
    console.log("共享内存已创建");
  });
}

// 获取内存使用情况并计算当前内存利用率
@Scenarios
function getMemoryInfo() {
  Memory().memoryType('local').operate('get_curdata').onGetData(function (result) {
    console.log("内存使用情况：" + result.usedMemory.toFixed(2) + 'GB/' 
      + result.totalMemory.toFixed(2) + "GB " + "当前内存利用率：" 
      + (result.usedMemory / result.totalMemory).toFixed(2) + '%');
  });
}

// 进行内容共享并设置共享范围
@Scenarios
function setShareVar() {
  Memory().memoryType('local').operate('set_data')
  .content({name: "Jack", age: 10, 5: true})
  .scope(['rs1', 'rs2']);
}

// 获取共享内容
@Scenarios
function getShareVar() {
  Memory().memoryType('local').operate('get_data')
  .content({name: null})
  .scope(['rs1']).onGetData(function (result) {
    console.log('name: ', result);
  });
}
```
{% endcode %}

#### 编译后TypeScript代码

{% code lineNumbers="true" %}
```typescript
// 创建共享内存区域
function createSharedMemory() {
  Memory.getInstance().name('testSharedMemory').size(256).onCreateSharedMemory(function() {
    console.log("共享内存已创建");
  }).build();
}

// 获取内存使用情况并计算当前内存利用率
function getMemoryInfo() {
  Memory.getInstance().memoryType('local').operate(['get_curdata']).onGetData(function (result) {
    console.log("内存使用情况: " + result.usedMemory.toFixed(2) + 'GB/' 
      + result.totalMemory.toFixed(2) + "GB " + "当前内存利用率: " 
      + (result.usedMemory / result.totalMemory).toFixed(2) + '%');
  }).build();
}

// 进行内容共享并设置共享范围
function setShareVar() {
  Memory.getInstance().memoryType('local').operate('set_data')
  .content({name: "Jack", age: 10, 5: true})
  .scope(['rs1', 'rs2'])).build();
}

// 获取共享内容
function getShareVar() {
  Memory.getInstance().memoryType('local').operate('get_data')
  .content({name: null})
  .scope(['rs1']).onGetData(function (result) {
    console.log('name: ', result);
  })).build();
}

// 内存性能监控
function memListenerStart() {
  memListener();
}
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="147">参数</th><th width="241">说明</th><th width="262">类型</th><th>备注</th></tr></thead><tbody><tr><td>memoryType</td><td>内存类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>内存相关操作</td><td>String[]</td><td>可选</td></tr><tr><td>scope</td><td>变量作用范围</td><td>String[]</td><td>可选</td></tr><tr><td>content</td><td>变量</td><td>Object</td><td>可选</td></tr><tr><td>name</td><td>共享内存名称</td><td>String</td><td>可选</td></tr><tr><td>size</td><td>共享内存大小</td><td>Int</td><td></td></tr><tr><td>prot</td><td>共享内存映射区域的权限</td><td>'Read' | 'Write' | 'Exec' | 'None'</td><td>可选</td></tr><tr><td>offset</td><td>共享内存映射区域的偏移量</td><td>Int</td><td>可选</td></tr><tr><td>length</td><td>共享内存映射区域的长度</td><td>Int</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="454">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr><tr><td>onCreateSharedMemory?(callback: (result: any) => void): void</td><td>使用提供的调试名称和大小创建匿名共享内存实例。该名称仅用于调试，并且可以在检查已映射此共享内存实例的进程的内存映射时帮助识别共享内存</td></tr><tr><td>onGetSharedMemorySize?(callback: (result: any) => void): void</td><td>返回共享内存的大小</td></tr><tr><td>onMap?(callback: (result: any) => void): void</td><td><p>创建共享内存映射的回调</p><p>使用指定的prot、偏移量和长度创建 共享内存的mmap。这将始终为后备共享内存区域生成一个新的 ByteBuffer窗口。当不再需要由map()返回的ByteBuffer时，对map()的每次调用都与对unmap(java.nio.ByteBuffer)的调用配对</p></td></tr><tr><td>onUnmap?(callback: (result: any) => void): void</td><td>取消共享内存映射的回调</td></tr><tr><td>onGetMemoryInfo?(callback: (result: any) => void): void</td><td>获取有关系统内存状态的信息</td></tr><tr><td>onGetProcessMemoryInfo?(callback: (result: any) => void): void</td><td>获取一个或多个进程的内存使用情况</td></tr></tbody></table>

