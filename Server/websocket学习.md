websocket的基本工作流程

1. 根据url指向的服务器及端口建立一个socket -(包涵ssl安全配置信息)
2. socket链接成功后才去http链接的方式获取链接头信息，并组装合法验证及链接升级为websocket长链接的数据，并通过socket链接发送到服务端进行验证
3. 通过socket获取http响应头数据，并验证数据响应的正确性，验证通过建立长链接，验证失败结束链接(要注意等待数据的响应完成，及资源占用与释放问题)。
4.链接成功后就可以进行消息的收发操作了。
