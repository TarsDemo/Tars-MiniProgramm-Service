# 案例服务的部署

本案例是一个简单的大学生活服务平台，接下来会介绍案例后端服务的部署，关于项目的具体信息可以查看[项目简介](/docs/Introduction.md)。

如果不清楚服务部署和发布流程或是还没有使用过Tars，请先看[创建第一个Tars应用](/docs/QuickStart.md)。

## 服务
本项目共有五个服务，包括一个数据服务，三个业务逻辑服务和一个接入服务，分别对应本项目下的五个目录，如下
```sh
.
├── DataServer          # 数据访问服务
├── UserInfoServer      # 用户信息服务
├── ClubActivityServer  # 社团活动服务
├── MessageWallServer   # 表白墙服务
└── InterfaceServer     # 接入服务
```

每个服务部署的步骤在每个服务目录的文档中都有详细说明，建议按照以下部署顺序部署服务

* [DataServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-DataServer/tree/release)
* [UserInfoServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-UserInfoServer/tree/release)
* [ClubActivityServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-ClubActivityServer/tree/release)
* [MessageWallServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-MessageWallServer)
* [InterfaceServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-InterfaceServer/tree/release)