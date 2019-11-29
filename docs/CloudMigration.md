# <a id="cloud"></a>上云
Tars框架和应用需要运行在Linux上，同时小程序的发布、上线也需要有符合要求的云环境，本节会讲述一个上云的完整流程。如果不打算上线发布应用，只想在本地服务器中尝试的话，可以跳过本部分，使用虚拟机代替。

* [云服务器购买](#server-purchase)
    * [腾讯云](#server-purchase-tencent-cloud)
    * [阿里云](#server-purchase-aliyun)
    * [AWS](#server-purchase-aws)
* [域名注册](#domain-registry)
    * [腾讯云](#domain-registry-tencent-cloud)
    * [阿里云](#domain-registry-aliyun)
* [域名解析](#dns)
    * [腾讯云](#dns-tencent-cloud)
    * [阿里云](#)
* [SSL证书](#ssl)
* [域名备案](#ba)
* [连接服务器](#connect-server)

## <a id="server-purchase"></a>云服务器购买
### <a id="server-purchase-tencent-cloud"></a>腾讯云
#### 登录
* 首先我们进入腾讯云首页(https://cloud.tencent.com)
![image](/docs/images/TencentCloudIndex.png)
* 点击右上角的登录，可以使用QQ或微信登录

#### 学生购买
* 如果是学生，可以点击中间的`云+校园扶持计划`，按照要求完成学生认证即可购买，学生每月只需要10元。
![](/docs/images/TencentCloudCampus.png)
* 地域根据自己需求选择即可，可以选择离自己最近的，系统选择`CentOS 7.5 64位`，配置不可选择，默认学生配置为`1核2GB`，已经足够使用了。
* 购买时长，可以根据自己需求，本案例中因为使用了小程序，需要备案，因此购买时长需要大于三个月

#### 非学生购买
* 非学生的话，需要通过主页顶部菜单栏的`产品>基础>计算>云服务器`进入云服务器页面，点击`立即选购`进入购买页面
![](/docs/images/TencentCloudBuyCvm.png)
* 机型配置方面，最低需要`1核2GB`，系统我们选择`CentOS 7.2`
* 购买时长，可以根据自己需求，本案例中因为使用了小程序，需要备案，因此购买时长需要大于三个月

#### 密码重置
* 服务器初始化使用的是随机生成的密码，我们可以重置服务器登录密码
* 点击主页右上角的`控制台`，可以进入自己的控制台看到自己购买的服务器信息
* 点击左侧Tab栏的`实例`，右侧会显示自己的服务实例
![](/docs/images/TencentCloudConsoleCvm.png)
* 点击实例的`操作>更多>密码/密钥>重置密码`，即可重置实例的root用户密码

### <a id="server-purchase-aliyun"></a>阿里云

#### 登录
* 进入阿里云首页(https://www.aliyun.com)
![](/docs/images/AliyunIndex.png)
* 点击上方的登录进入登录页，可以使用淘宝、支付宝等账号登录

#### 学生购买
* 进入[云翼计划](https://promotion.aliyun.com/ntms/act/campus2018.html)页面
![](/docs/images/AliyunCampus.png)
* 完成学生认证即可购买，每月9.5元
* 系统选择`CentOS 7.3 64`，地域根据自己需求选择，可以选择离自己较近的
* 默认配置为`1核2G`

#### 非学生购买
* 点击首页顶部`产品分类>云计算基础>弹性计算>云服务器>云服务器 ECS`，进入云服务器页面点击`立即购买`进入购买选择页
![](/docs/images/AliyunBuyEcs.png)
* 系统类型选择`CentOS`，版本选择7以上即可
* 配置上，选择内存2G以上的实例即可

#### 密码重置
* 点击顶部的控制台进入控制台页面
* 点击左侧Tab的`云服务器 ECS`，进入云服务器管理页面
* 点击左侧Tab栏中的`实例`，右侧展示自己的实例信息
![](/docs/images/AliyunConsole.png)
* 点击实例的`操作>更多>密码/密钥>重置实例密码`，即可重置实例密码
![](/docs/images/AliyunConsoleEcs.png)

<!-- ### <a id="server-purchase-aws"></a> AWS
打开[AWS主页](https://aws.amazon.com/cn/)，没有账号可以点击右上角`创建AWS账户`创建账号，登录后可以点击主页上的免费套餐，AWS新注册账号部分产品可以免费使用一年，但是配置会比较低。
![](/docs/images/CloudMigrationAWSIndex.png) -->


## <a id="domain-registry"></a>域名注册
### <a id="domain-registry-tencent-cloud"></a>腾讯云
#### 在主页找到`产品>企业应用>域名注册`打开域名注册页
![](/docs/images/CloudMigrationTencentCloudIndexToDomain.png)

#### 输入自己需要或喜欢的域名进行搜索
![](/docs/images/CloudMigrationTencentCloudDomainSearch.png)

#### 然后从搜索结果中选取自己喜欢的并且没有被注册的域名点击`加入购物车`并点击右侧的`立即购买`。
> 一般`com`和`cn`域名会贵一些，`xyz`, `club`等会便宜一些

![](/docs/images/CloudMigrationTencentCloudDomainSelect.png)

#### 提交订单时，用户类型选择`个人用户`，并按照要求填写个人信息，再点击`提交订单`，付款即完成域名注册
![](/docs/images/CloudMigrationTencentCloudDomainBuying.png)

### <a id="domain-registry-aliyun"></a>阿里云
#### 在主页找到`产品分类>企业应用>域名注册`打开域名注册页
![](/docs/images/CloudMigrationAliyunIndexToDomain.png)

#### 输入自己需要或喜欢的域名进行搜索
![](/docs/images/CloudMigrationAliyunDomainSearch.png)

#### 然后从搜索结果中选取自己喜欢的并且没有被注册的域名点击`加入清单`并点击右侧的`立即结算`。
![](/docs/images/CloudMigrationAliyunDomainSelect.png)

#### 提交订单时，域名持有者选择`个人`，点`创建信息模板`并按照要求填写个人信息，再点击`立即购买`，付款即完成域名注册
![](/docs/images/CloudMigrationAliyunDomainBuying.png)

## <a id="dns"></a>域名解析
域名和服务器之间目前是没有关系的，无法通过域名找到我们的服务器。而域名解析可以将域名解析到对应IP的服务器上。
### <a id="dns-tencent-cloud"></a>腾讯云
#### 解析套餐购买
一个账号一般可以购买一个免费的解析套餐，我们通过主页的`产品>企业应用>云解析`进入解析套餐购买页，并点击`立即购买`

![](/docs/images/CloudMigrationTencentCloudTodns.png)

在购买页如果是账号第一次购买，可以选择免费版套餐，点击`核对信息并支付`完成付款即购买完成

![](/docs/images/CloudMigrationTencentClouddnsBuying.png)

#### 域名解析设置
进入控制台，找到`云解析`，进入云解析控制台界面

![](/docs/images/CloudMigrationTencentCloudTodnsConsole.png)

然后点击`添加解析`，输入购买的需要解析的域名，点击确认，列表中就会显示刚刚添加的解析域名，然后在`操作`中点击`解析`，进入域名的解析配置页

![](/docs/images/CloudMigrationTencentCloudAddDNS.png)

点击`添加记录`，添加域名的解析规则

![](/docs/images/CloudMigrationTencentCloudDNSSetting.png)

我们添加如下的解析规则，主机记录即域名前缀，选`www`，就会对`www.tarsdemo.com`进行解析。

然后记录值填写我们购买的服务器地址，保存后因为TTL为600，需要等十分钟配置才会生效，十分钟后就可以通过域名找到我们的服务器了

![](/docs/images/CloudMigrationTencentCloudDNSSettingContent.png)

可以使用`nslookup`命令验证域名是否成功解析（Linux/MacOS的终端和Windows的cmd都可用），如
```sh
nslookup www.tarsdemo.com
```

### <a id="dns-aliyun"></a>阿里云
待完善……

## <a id="connect-server"></a>连接服务器

服务器可以使用`ssh`协议来远程连接，不同的系统使用的工具不太一样

### Windows 连接到服务器

由于Win10以前的Windows版本没有内置OpenSSH，连接服务器时需要使用额外的连接工具，工具的种类也有很多，比如`XShell`, `PuTTY`等，使用上基本大同小异，可以搜索一下使用方法。

在进行连接时，在主机名(Host Name或IP Address)栏中填写服务器的公网IP，端口一般为默认的`22`，用户名一般为`root`，密码即为上一节中我们购买服务器后重置的密码，然后连接就能够进入服务器的终端界面了。

### MacOS, Linux 连接到服务器

在macOS和Linux中，我们只需要打开终端(Terminal)，使用`ssh`命令连接服务器即可，如下（Win10中也可以在CMD中使用相同的命令连接）
```sh
ssh root@${IP地址} -p ${端口}
```
例如连接到公网IP为`1.2.3.4`的服务器，`ssh`使用的端口是`3366`
```sh
ssh root@1.2.3.4 -p 3366
```
回车后输入密码即可进入服务器终端，进行Tars框架安装、应用开发、部署等操作。