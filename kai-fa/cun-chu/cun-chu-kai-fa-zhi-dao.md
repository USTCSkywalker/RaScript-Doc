# 存储开发指导

#### 示例代码

{% code lineNumbers="true" %}
```typescript
  @Scenarios
  function queryDB() {
    Storage(storage_query).onQuery(function (res) {
      console.log("查询结果为: ");
      res.forEach((object, index) => {
        console.log(`Object at index ${index}:`, object);
      });
    });
  }
  
  @Scenarios
  function readFile() {
    File(file_read).onRead(function () {
      console.log("用户的readFile回调函数");
    });
  }
```
{% endcode %}

#### 静态属性

<table><thead><tr><th width="192">参数（StorageAttr）</th><th width="364">说明</th><th width="94">类型</th><th>备注</th></tr></thead><tbody><tr><td>storageType</td><td>存储类型：DB、文件、SP</td><td>String</td><td></td></tr><tr><td>operation</td><td>操作类型：增、删、改、查</td><td>String[]</td><td>可选</td></tr><tr><td>dbPath</td><td>存储路径：以Uri的方式描述DB路径</td><td>String</td><td></td></tr><tr><td>schema</td><td>数据库Schema</td><td>any[]</td><td>可选</td></tr><tr><td>schemaVersion</td><td>数据库Schema版本</td><td>Number</td><td></td></tr><tr><td>name</td><td>存储命名</td><td>String</td><td>可选</td></tr></tbody></table>

<table><thead><tr><th width="193">参数（FileAttr）</th><th width="364">说明</th><th width="93">类型</th><th>备注</th></tr></thead><tbody><tr><td>fileType</td><td>文件类型</td><td>String</td><td></td></tr><tr><td>filename</td><td>文件名</td><td>String</td><td></td></tr><tr><td>operation</td><td>文件操作</td><td>String[]</td><td>可选</td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="424">抽象动作（StorageAction）</th><th>说明</th></tr></thead><tbody><tr><td>onCreate?(callback: (result: any) => void): void</td><td>DB创建回调</td></tr><tr><td>onInsert?(callback: () => object): void</td><td>DB数据插入回调</td></tr><tr><td>onSuccess?(callback: (result: any) => object): void</td><td>操作成功回调</td></tr><tr><td>onFail?(callback: (result: any) => object): void</td><td>操作失败回调</td></tr></tbody></table>

<table><thead><tr><th width="425">抽象动作（FileAction）</th><th>说明</th></tr></thead><tbody><tr><td>onCreate?(callback: () => void): void</td><td>文件创建回调</td></tr><tr><td>onRead?(callback: () => void): void</td><td>文件读取回调</td></tr><tr><td>onWrite?(callback: () => string): void</td><td>文件写入回调</td></tr><tr><td>onDelete?(callback: () => void): void</td><td>文件删除回调</td></tr><tr><td>onSuccess?(callback: () => object): void</td><td>操作成功回调</td></tr><tr><td>onFail?(callback: () => object): void</td><td>操作失败回调</td></tr></tbody></table>
