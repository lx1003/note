#### OAuth2的四个角色

1. Resource Owner：资源拥有者
2. Resource Server：资源服务器
3. Client：第三方应用客户端
4. Authorization Server：授权服务器，管理Resource Owner，Client、和Resource Server的三角关系的中间层

其中Authorization Server和Resource Server可以是独立的服务提供商，也可以是在一起的

OAuth2解决问题的关键在于使用Authorization Server提供一个访问凭证给Client，使得Client可以在不知道Resource owner在Resource server上的用户名和密码的情况下消费Resource owner的受保护资源

#### 部署OAuth2需要的完成的工作

1. 增加一个Authorization Server，提供授权的实现，一般由Resource Server来提供
2. Resource Server为第三方应用程序提供注册接口
3. Resource Server开放相应的受保护资源的API
4. Client注册成为Resource Server的第三方应用
5. Client消费这些API

作为资源服务提供商来说，1，2，3这三件事情是需要完成的

作为第三方应用程序，要完成的工作是在4和5这两个步骤中

其中作为Resource owner来说，是不用做什么的，是OAuth2受益的千千万万的最终人类用户

##### 作为Resource Server

在一般情况下，Resource Server提供Authorization Server服务，主要提供两类接口：

1. 授权接口：接受Client的授权请求，引导用户到Resouce Server完成登陆授权的过程
2. 获取访问令牌接口：使用授权接口提供的许可凭证来颁发Resource owner的访问令牌给Client，或者由Clent更新过期的访问令牌

1. client_id：第三方应用程序的一个标识ID，这个信息通常是公开的信息，用来区分哪一个第三方应用程序
2. client_secret：第三方应用程序的私钥信息，这个信息是私密的信息，不允许在OAuth2流程中传递的，用于安全方面的检测和加密

##### 作为Client

在Client取得client_id和client_secret之后，使用这些信息发起授权请求、获取access_token请求和消费受保护的资源 ![OAuth2授权流程](..\images\OAuth2授权流程.png)