# Deploy Demo Services

[中文版](/docs/DeployDemo.md)

This demo is a simple college life service platform. This document will introduce how to deploy the backend services. About the detail of this project, refer to [Introduction](/docs/Introduction_en.md).

If you don't know how th deploy and publish service, or haven't used TARS, refer to [Create Your First TARS Application](/docs/QuickStart_en.md).

## Services

This demo has 5 services, which include a data service, three logic services and a interface service.

```sh
.
├── DataServer          # Data service
├── UserInfoServer      # User information service
├── ClubActivityServer  # Club activity event service
├── MessageWallServer   # Message wall service
└── InterfaceServer     # Interface service
```

The steps of each service deployment are detailed in the documentation of each service catalog. It is recommended to deploy the services in the following deployment order

* [DataServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-DataServer/tree/release)
* [UserInfoServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-UserInfoServer/tree/release)
* [ClubActivityServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-ClubActivityServer/tree/release)
* [MessageWallServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-MessageWallServer)
* [InterfaceServer](https://github.com/TarsDemo/Tars-MiniProgramm-Service-InterfaceServer/tree/release)