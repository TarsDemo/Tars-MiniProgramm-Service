# <a id="introduction"></a> Introduction

[中文版](/docs/Introduction.md)

A Life Service Platform applet for college students, which uses WeChat Miniprogram as frontend (WePY framework and vant component), and TARS as backend (Tars.js, TarsGo, TarsCpp), and MySQL as database.

## <a id="introduction-function"></a> Functions

This app has three modules: user module, message wall module and club event module. The functions of each module are as the following

![](/docs/images/IntroductionFunction.png)
<!-- <img width="500" src="https://github.com/ETZhangSX/LifeService/blob/master/docs/images/IntroductionFunction.png?raw=true"> -->

## <a id="ui"></a> UI

![](/docs/images/IntroductionUI.png)

## <a id="introduction-structure"></a> Structure

```sh
.
├── DataServer          # Data access service
├── ClubActivityServer  # Club event management service
├── UserInfoServer      # user information service
├── MessageWallServer   # message wall service
├── InterfaceServer     # access layer service
├── docs/images         # documents and images source
└── README.md
```

## <a id="introduction-logic-architecture"></a> Application Architechture

The architechture of this application is as following

![image](/docs/images/logicArchitecture.png)

Each module of miniprogram uses HTTPS to interact with the access layer. User module achieves WeChat login by using the WeChat API proxy in access layer to obtain `openID` of users. And the others call the service in other layer through the access layer.

## <a id="introduction-deploy-architecture"></a> Deployment Architechture

We deployed the services in two servers. the blue part presents the miniprogram, with orange for the deployed services and green for the TARS framework.

![image](/docs/images/DataArchitecture.jpg)

Server management interaction relationship is as following:

![image](/docs/images/ManagementArchitecture.jpg)