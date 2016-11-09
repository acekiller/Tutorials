Perfect 服务器开发教程

截止目前，Perfect要求的swift最低版本为3.0。
So, 检查一下版本是否为正确吧:
swift --version
如果版本过低请先自行升级吧。

做好这些之后就可以开始服务器开发了。我们直接基于提供的模版来进行开发吧：
git clone https://github.com/PerfectlySoft/PerfectTemplate.git
clone好模版后，我们就需要进行编译了：
swift build
在编译过程中，由于Perfect开发的Lib还不存在需要从网络上下载，因此会比较慢。
好吧，我们先放松一下。
...
接下来，执行
.build/debug/PerfectTemplate
程序就启动起来了。

这样我们就可以通过网络访问了。
一个几本的服务器就搭建好了。

等等，现在的苹果都要求要给予https进行项目开发了，那么。我们该怎么做呢？
目前自己在文档上并没有查到相关的说明。大概看了一下HTTPServer.swift文件
里面有
public func start(port: UInt16, sslCert: String, sslKey: String, bindAddress: String = "0.0.0.0")
public func start()
两个函数。并且对
public func start(port: UInt16, sslCert: String, sslKey: String, bindAddress: String = "0.0.0.0")
做了如下标记：
@available(*, deprecated, message: "Set serverPort and ssl directly then call start()")
这告诉我们这个函数已经废弃掉了。我们可以通过直接设置serverPort 和 ssl,然后执行start()
接下来，就看了一下ssl属性，原来是一个元组。包含了两个字符串。
到这里我们基本上已经明白了，我们需要做的就是配置一个sslCert和sslKey。要说明这里要配置的是这两个文件能够查找的文件路径。
不过对于这个路径我们可以按照工程的相对路径进行配置。配置好后执行上面的编译和执行操作。一切几本就OK了。
