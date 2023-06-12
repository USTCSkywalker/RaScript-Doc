# 场景配置

场景配置是通过@Scenarios装饰function来实现，function被@Scenarios装饰后具有管理资源的能力。@Scenarios的参数是可选的，参数用来指定场景模式，如 Call：通话模式；EnergySaving：节能模式。&#x20;

编译器会根据@Scenarios，提取当前函数的场景模式，同时对场景内的抽象资源进行构建和调用。运行时会对场景调用进行自适应匹配。

{% code lineNumbers="true" %}
```typescript
// 默认的startRecording
@Scenarios
    function startRecording() {
    }
// EnergySaving, Call场景模式下的startRecording
@Scenarios(EnergySaving, Call)
    function startRecording() {
    }
```
{% endcode %}
