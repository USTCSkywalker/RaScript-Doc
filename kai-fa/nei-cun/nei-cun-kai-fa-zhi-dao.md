# 内存开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
@Scenarios
function getMemoryInfo() {
    Memory().memoryType('local').operate('get_curdata').onGetData(function (result) {
      console.log("内存使用情况: " + result.usedMemory.toFixed(2) + 'GB/' + result.totalMemory.toFixed(2) + "GB "
        + "当前内存利用率: " + (result.usedMemory / result.totalMemory).toFixed(2) + '%'
      );
    });
  }
  
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

#### 静态属性

<table><thead><tr><th width="147">参数</th><th width="412">说明</th><th width="90">类型</th><th>备注</th></tr></thead><tbody><tr><td>memoryType</td><td>内存类型</td><td>String</td><td></td></tr><tr><td>operation</td><td>内存捕获操作</td><td>String[]</td><td>可选</td></tr><tr><td>scope</td><td>变量作用范围</td><td>String[]</td><td>可选</td></tr><tr><td>content</td><td>变量</td><td>object</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="407">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onGetData?(callback: (result: any) => void): void</td><td>获取当前数据</td></tr></tbody></table>

