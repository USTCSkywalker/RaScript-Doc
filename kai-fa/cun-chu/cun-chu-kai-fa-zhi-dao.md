# 存储开发指导

#### 静态属性

{% code lineNumbers="true" %}
```typescript
StoreAttr {
    storeId : Number,    // 存储类型：DB、⽂件、SP
    storeIdPath : String,    // 存储路径：以Uri的⽅式描述DB路径、⽂件路径
    actionId : Number,    // 操作类型：增删改查
}
```
{% endcode %}

#### 抽象动作

{% code lineNumbers="true" %}
```typescript
onRfile ? : (result : any)=>void    // 读取文件回调
onWfile ? : (file : File)=>void    // 写⼊回调，再回调中向file写⼊数据
onOpenDB ? : (result: String)=>void    // DB打开回调
onInsterDBData ? : (result: InsterObject))=>void    // DB数据插⼊回调
onUpdateDBData ? : (result: UpdateObject))=>void    // DB数据更新回调
onDeleteDBData ? : (result: String))=>void    // DB数据删除回调
onSelectDBData ? : (result : any)=>void    // DB数据选择回调
onCreatDBTable ? : (result: String))=>void    // DB创建表回调
onDeleteDBTable ? : (result: String))=>void    // DB删除表回调
onCreatDB ? : (result: String))=>void    // DB创建回调
onDeleteDB ? : ()=>void    // DB删除回调
onCloseDB ? : (result: String)=>void    // DB关闭回调
```
{% endcode %}
