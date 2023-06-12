# 数据处理

RaScript通过阻塞队列实现流式数据连续有序传递，通过消息订阅分发机制实现单次数据全局传递。其他数据管理，如资源数据和UI，及应用全局的数据管理，可复用UI框架提供的数据管理能力。

#### 连续有序传递

useQueue\<T>():

enqueue(t: T);

dequeue();

isEmpty();

阻塞队列，传入数据类型，进行入队和出队等操作

#### 单次消息订阅分发

useMesseage\<T>():

regist(key : String, fun : Function);

emit(key : String, value : T));

注册监听，发送消息，进行全局消息分发
