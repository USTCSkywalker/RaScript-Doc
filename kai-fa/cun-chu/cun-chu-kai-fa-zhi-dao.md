# 存储开发指导

#### 静态属性

<table><thead><tr><th width="136">参数</th><th width="404">说明</th><th width="107">类型</th><th>备注</th></tr></thead><tbody><tr><td>storeId</td><td>存储类型：DB、文件、SP</td><td>Number</td><td></td></tr><tr><td>storeIdPath</td><td>存储路径：以Uri的方式描述DB路径、文件路径</td><td>String</td><td></td></tr><tr><td>actionId</td><td>操作类型：增、删、改、查</td><td>Number</td><td></td></tr></tbody></table>

#### 抽象动作

<table><thead><tr><th width="437">抽象动作</th><th>说明</th></tr></thead><tbody><tr><td>onRfile ? : (result : any) => void</td><td>读取文件回调</td></tr><tr><td>onWfile ? : (file : File) => void</td><td>写入回调，再回调中向file写入数据</td></tr><tr><td>onOpenDB ? : (result: String) => void</td><td>DB打开回调</td></tr><tr><td>onInsterDBData ? : (result: InsterObject)) => void</td><td>DB数据插入回调</td></tr><tr><td>onUpdateDBData ? : (result: UpdateObject)) => void</td><td>DB数据更新回调</td></tr><tr><td>onDeleteDBData ? : (result: String)) => void</td><td>DB数据删除回调</td></tr><tr><td>onSelectDBData ? : (result : any) => void</td><td>DB数据选择回调</td></tr><tr><td>onCreateDBTable ? : (result: String)) => void</td><td>DB创建表回调</td></tr><tr><td>onDeleteDBTable ? : (result: String)) => void</td><td>DB删除表回调</td></tr><tr><td>onCreatDB ? : (result: String)) => void</td><td>DB创建回调</td></tr><tr><td>onDeleteDB ? : () => void</td><td>DB删除回调</td></tr><tr><td>onCloseDB ? : (result: String) => void</td><td>DB关闭回调</td></tr></tbody></table>
