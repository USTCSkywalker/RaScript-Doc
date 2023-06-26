# 过程流型资源

#### 通用动作

可用资源列表

{% code lineNumbers="true" fullWidth="false" %}
```typescript
onDeviceList ? : (result: List<T>)=>void: void // 所有可用资源列表回调
```
{% endcode %}

原始数据流获取

{% code lineNumbers="true" %}
```typescript
onOriginData ? : (result : any)=>void : void  // 设备原始数据流
```
{% endcode %}

获得最新一次数据

<pre class="language-typescript"><code class="lang-typescript"><strong>onGetData?(callback: (result: any) => void): void //获取当前数据
</strong></code></pre>

设备打开

{% code lineNumbers="true" %}
```typescript
onOpen ? : (result: String)=>void: void    // 设备打开时的回调
```
{% endcode %}

设备关闭

{% code lineNumbers="true" %}
```typescript
onStop ? : (result: String)=>void: void    // 设备关闭时的回调
```
{% endcode %}
