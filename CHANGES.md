# V3版本(v3分支)
## 版本特性

- 全面使用Handler处理封包接收,发送, 解析, 日志, RPC等结构

- 新增编码器扩展, 支持混合编码器

- 新增socket的各种属性设置, 超时处理等

- 新的计时器api

- 新增WebSocket支持

- 底层采用性能更高的纯二进制协议进行错误及rpc消息传输


## 变化及修改

- 底层去除Protobuf协议依赖(依然支持Protobuf)

- 大幅降低底层内存分配, GC降低后, benchmark IOPS提升

- 现在使用cellnet.RegisterMessage注册消息, 回调参数统一为*Event

- 去除RPC包装, 解包封包的重复代码. 封包变小

- 编码解码过程放到线程中处理, 提升性能




# V2版本(v2分支)

## 版本特性

- 实现单线程逻辑时, 全局只有1个EventQueue. 而不是一个Peer一个Queue

- EventDispatcher处理回调

- 处理DB, Timer等不依赖Dispatcher(Peer)逻辑时, 在Post时, Dispatcher可以指定nil, 通过data的函数得到异步返回

- 去掉MongoDB支持


## 变化及修改

- 去掉V1中的EventPipe

- V1中的EventQueue被拆成EventDispatcher及新的EventQueue

- 新的EventQueue实现了EventPipe的一部分功能

- 调整EventQueue的Post命名及DelayPost的参数

- 去掉PeerEvent支持

- socket.RegisterEventMessage改为socket.RegisterMessage

- 例子/测试用例使用sample文件夹命名

# V1版本(v1分支)