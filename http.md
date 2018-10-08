> ### URL 和 URI

URI: 由某个协议方案表示的资源的定位标识符，协议方案是指协议类型（例如http协议

Uniform: 规定统一格式方便处理多种不同类型的资源，且新增协议也方便

Resource：资源的定义是可标识的任何东西，除了文档文件、图像或者服务（天气）等能够区别于其他类型的，全都可作为资源，可以是集合体

Identifier：可标识对象，即标识符


URI用字符串标识某一互联网资源，URL表示资源的地点（互联网具体位置），所以URL是URI的子集。

### http/1.0

http本身是无状态协议，它自身不保存请求和响应之间的通信状态。http协议对于发送过的请求或者响应不做持久化处理

原因：这是为了更快地处理大量事务，确保协议的可伸缩性。

### http/1.1

也是无状态协议，但是为了实现期望的保存状态，引入了cookie进行状态管理

### 持久化连接

背景：每一次http通信都需要进行一次tcp的连接和断开，大量http请求时需要进行大量的tcp连接，增加通信量的开销

特点：只要任意一端没有明确提出断开连接，则保持tcp的连接状态

协议：http/1.1默认都是持久化连接。hhtp/1.0并未标准化，需要两端进行设置实现持久连接

影响：让多个请求能够以 管线化 方式进行发送，不需要等待响应即可进行下一次的请求发送