# <a id="introduction"></a>项目简介

[English Version](/docs/Introduction_en.md)

学生校园生活服务平台小程序，前端为微信小程序（WePY 框架和 vant 组件）；后端使用了 TARS 微服务框架 (Tars.js, TarsGo, TarsCpp)；数据库使用了 MySQL。

## <a id="introduction-function"></a>功能

小程序可以分为三个功能模块，用户模块、表白墙、社团活动，各模块包含的具体功能如下
![](/docs/images/IntroductionFunction.png)
<!-- <img width="500" src="https://github.com/ETZhangSX/LifeService/blob/master/docs/images/IntroductionFunction.png?raw=true"> -->

## <a id="ui"></a> 小程序 UI

![](/docs/images/IntroductionUI.png)

## <a id="introduction-structure"></a>项目结构

```sh
.
├── DataServer          # 数据访问服务
├── ClubActivityServer  # 社团活动服务
├── UserInfoServer      # 用户信息服务
├── MessageWallServer   # 表白墙服务
├── InterfaceServer     # 接入服务
├── docs/images         # 文档图片
└── README.md
```

## <a id="introduction-logic-architecture"></a>项目逻辑架构

小程序的前后端逻辑架构如下

![image](/docs/images/logicArchitecture.png)

小程序端各模块的功能通过 HTTPS 请求和接入层交互，其中用户模块中的微信登录功能通过接入层的微信 API 代理调用微信 API 获取用户 `openID`，其它功能通过接入服务调用服务层的服务接口。
## <a id="introduction-deploy-architecture"></a>项目部署架构

实际部署部署，采用普通 PC 做为前端设备，将具体应用部署在两台服务器上。 其中蓝色表示部署前端小程序, 橘黄色表示部署的应用服务, 绿色表示 TARS 服务框架.

其中值得说明的是: 我们将 `ClubActivityServer`, `MessageWallServer`, `UserInfoServer` 三个服务分别部署在 2 台服务器上, 实现业务符合分担和高可靠谱性. 

![image](/docs/images/DataArchitecture.jpg)

管理面交互情况如下：
![image](/docs/images/ManagementArchitecture.jpg)