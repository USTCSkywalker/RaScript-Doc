# CPU开发概述

RaScript可以获取性能指标，像“Perf Monitor”一样监控如UI线程FPS、JS线程FPS和CPU占用率。

#### 约束与限制

* 监控到的FPS可能与在“Perf Monitor”中看到的不完全匹配。然而，这些值彼此接近，并展现出相同的变化趋势。 这是因为在原生impl中每500毫秒刷新一次FPS数据（“Perf Monitor”也是如此）。RaScript可能在“Perf Monitor”之外的另一个时间点开始跟踪本机性能统计数据，因此它们会在不同的时刻获取到刷新的数据。
