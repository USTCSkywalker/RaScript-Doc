# 异常处理能力

Framework层的管理类已经内置了异常处理措施，如果用户需要获取异常信息做定制化处理，可通过 onError(errcode : Number, errProcess : ErrorProcess)对返回的错误码进行判断并处理。&#x20;

常见errcode:

{% code lineNumbers="true" %}
```
PERMISSION_INVAILD    // 权限异常
DEVICE_INVAILD    // 设备缺失
DEVICE_OPEN_ERROR    // 设备打开异常
DEVICE_STATE_ERROR    // 设备状态异常
DEVICE_CLOSE_ERROR    // 设备关闭异常
DATA_GET_ERROR    // 数据获取异常
DATA_SEND_ERROR    // 数据发送异常
DATA_PROCESS_ERROR    // 数据转换异常
IO_ERROR    // IO异常
```
{% endcode %}

ErrorProcess提供用户定制化的异常处理方式

{% code lineNumbers="true" %}
```
retry(opd : Number, n : Number)
finish()
skip(opd : Number)
```
{% endcode %}

使用示例

{% code lineNumbers="true" fullWidth="false" %}
```typescript
Camera(camera_preview).onError((errcode : Number, errProcess : ErrorProcess) => {
    switch(errcode):
        case PERMISSION_INVAILD : errProcess.retry(PERMISSION, 1);
        case DEVICE_STATE_ERROR : errProcess.skip(PREVIEW);
        case IO_ERROR : errProcess.finish();
        case DATA_SEND_ERROR : console.log("发送失败");
});
```
{% endcode %}
