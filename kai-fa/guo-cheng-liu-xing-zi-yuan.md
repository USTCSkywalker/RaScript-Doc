# 过程流型资源

#### 通用动作

可用资源列表

{% code lineNumbers="true" fullWidth="false" %}
```typescript
onDeviceList ? : (result: List<T>)=>void    // 所有可用资源列表回调
```
{% endcode %}

原始数据流获取

{% code lineNumbers="true" %}
```typescript
onOriginData ? : (result : any)=>void    // 设备原始数据流
```
{% endcode %}

设备打开

{% code lineNumbers="true" %}
```typescript
onOpen ? : (result: String)=>void    // 设备打开时的回调
```
{% endcode %}

设备关闭

{% code lineNumbers="true" %}
```typescript
onClose ? : (result: String)=>void    // 设备关闭时的回调
```
{% endcode %}
