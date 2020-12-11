# <a id="cloud"></a>Cloud Migration

[中文版](docs/CloudMigration.md)

The TARS framework and applications need to run on Linux. At the same time, the release and launch of WeCaht applets also need a cloud environment that meets the requirements. This section will describe a complete process of going to the cloud. If you don't plan to publish the application online, but just want to try it on the local server, you can skip this section and use a virtual machine instead.

* [Cloud server purchase](#server-purchase)
    * [Tencent Cloud](#server-purchase-tencent-cloud)
    * [Aliyun](#server-purchase-aliyun)
    * [AWS](#server-purchase-aws)
* [Domain registration](#domain-registry)
    * [Tencent Cloud](#domain-registry-tencent-cloud)
    * [Aliyun](#domain-registry-aliyun)
* [DNS](#dns)
    * [Tencent Cloud](#dns-tencent-cloud)
    * [Aliyun](#)
* [SSL certificate](#ssl)
* [Domain name registration](#ba)
* [Connect to the server](#connect-server)

## <a id="server-purchase"></a>Cloud server purchase
### <a id="server-purchase-tencent-cloud"></a>Tencent Cloud
#### Login

* First we enter the Tencent Cloud homepage.(https://cloud.tencent.com)
![image](/docs/images/TencentCloudIndex.png)
* Click login in the upper right corner, you can log in using QQ or WeChat.

#### Purchase

* We need to enter the cloud server page through `Product>Basics>Compute>Cloud Server` in the menu bar at the top of the homepage, and click `Shop Now` to enter the purchase page
![](/docs/images/TencentCloudBuyCvm.png)
* In terms of model configuration, the minimum requirement is `1 core 2GB`, and we choose `CentOS 7.2` for the system
* The purchase time can be based on your own needs. In this case, because a small program is used, it needs to be filed, so the purchase time needs to be more than three months.

#### Reset Password

* The server initialization uses a randomly generated password, we can reset the server login password.
* Click on the `console` in the upper right corner of the homepage, you can enter your console to see the server information you purchased.
* Click the `instance` in the Tab bar on the left, and your service instance will be displayed on the right
![](/docs/images/TencentCloudConsoleCvm.png)
* Click on the instance's `Operation>More>Password/Key>Reset Password` to reset the root user password of the instance.

### <a id="server-purchase-aliyun"></a>Aliyun

#### Login

* Enter Aliyun homepage(https://www.aliyun.com)
![](/docs/images/AliyunIndex.png)
* Click login above to enter the login page, you can log in with Taobao, Alipay and other accounts.

#### Puechase

* Click on the top of the homepage `Product Category>Basic Cloud Computing>Elastic Computing>Cloud Server>Cloud Server ECS`, enter the cloud server page and click `Buy Now` to enter the purchase selection page.
![](/docs/images/AliyunBuyEcs.png)
* System type is `CentOS`, version is `7` or above
* For configuration, select an instance with memory above `2G`

#### Reset Password
* Click on the console at the top to enter the console page.
* Click `Cloud Server ECS` on the left Tab to enter the cloud server management page.
* Click the `instance` in the Tab bar on the left, and display your own instance information on the right.
![](/docs/images/AliyunConsole.png)
* Click on the instance's `operations>more>password/key>reset instance password` to reset the instance password.
![](/docs/images/AliyunConsoleEcs.png)

<!-- ### <a id="server-purchase-aws"></a> AWS
打开[AWS主页](https://aws.amazon.com/cn/)，没有账号可以点击右上角`创建AWS账户`创建账号，登录后可以点击主页上的免费套餐，AWS新注册账号部分产品可以免费使用一年，但是配置会比较低。
![](/docs/images/CloudMigrationAWSIndex.png) -->


## <a id="domain-registry"></a>Domain registration
### <a id="domain-registry-tencent-cloud"></a>Tencent Cloud
#### Find `Product>Enterprise Application>Domain Registration` on the homepage to open the domain name registration page.
![](/docs/images/CloudMigrationTencentCloudIndexToDomain.png)

#### Enter the domain name you need or like to search
![](/docs/images/CloudMigrationTencentCloudDomainSearch.png)

#### Then select the domain name you like and not registered from the search results, click `Add to shopping cart` and click `Buy now` on the right.

> Generally, `com` and `cn` domain names are more expensive, while `xyz`, `club` etc. are cheaper.

![](/docs/images/CloudMigrationTencentCloudDomainSelect.png)

#### When submitting an order, select the user type `individual user`, fill in personal information as required, and then click `submit order` to complete the domain name registration after payment.
![](/docs/images/CloudMigrationTencentCloudDomainBuying.png)

### <a id="domain-registry-aliyun"></a>Aliyun
#### Find `Product Category>Enterprise Application>Domain Registration` on the homepage to open the domain name registration page.
![](/docs/images/CloudMigrationAliyunIndexToDomain.png)

#### Enter the domain name you need or like to search.
![](/docs/images/CloudMigrationAliyunDomainSearch.png)

#### Then select the domain name you like and has not been registered from the search results, click `Add to list` and click `Check out now` on the right.
![](/docs/images/CloudMigrationAliyunDomainSelect.png)

#### When submitting the order, the domain name holder selects `personal`, clicks `create information template` and fills in personal information as required, and then clicks `buy now` to complete the domain name registration after payment.
![](/docs/images/CloudMigrationAliyunDomainBuying.png)

## <a id="dns"></a>DNS
There is currently no relationship between the domain name and the server, and our server cannot be found through the domain name. The domain name resolution can resolve the domain name to the server corresponding to the IP.

### <a id="dns-tencent-cloud"></a>Tencent Cloud
#### Analysis package purchase

An account can generally purchase a free parsing package. We go to the parsing package purchase page through `Products>Enterprise Applications>Cloud DNS` on the homepage, and click `Buy Now`.

![](/docs/images/CloudMigrationTencentCloudTodns.png)

On the purchase page, if it is the first purchase of the account, you can choose the free version package, click on `check information and pay` to complete the payment to complete the purchase.

![](/docs/images/CloudMigrationTencentClouddnsBuying.png)

#### DNS Configuration

Enter the console, find `Cloud Resolution`, enter the Cloud Resolution console interface.

![](/docs/images/CloudMigrationTencentCloudTodnsConsole.png)

Then click `Add Resolution`, enter the purchased domain name that needs to be resolved, and click Confirm. The newly added resolution domain name will be displayed in the list, and then click `Resolve` in the `Operation` to enter the domain name resolution configuration page.

![](/docs/images/CloudMigrationTencentCloudAddDNS.png)

Click `Add Record` to add the domain name resolution rule.

![](/docs/images/CloudMigrationTencentCloudDNSSetting.png)

We add the following parsing rules, the host record is the domain name prefix, select `www`, and `www.tarsdemo.com` will be resolved.

Then record the value and fill in the server address we purchased. After saving, because the TTL is `600`, it takes ten minutes for the configuration to take effect. After ten minutes, we can find our server through the domain name.

![](/docs/images/CloudMigrationTencentCloudDNSSettingContent.png)

You can use the `nslookup` command to verify whether the domain name is successfully resolved (Linux/MacOS terminal and Windows cmd are available), such as

```sh
nslookup www.tarsdemo.com
```

### <a id="dns-aliyun"></a>Aliyun
To be perfected……

## <a id="ssl"></a>SSL certificate
### <a id="ssl-tencent-cloud"></a>Tencent Cloud

On the Tencent Cloud homepage, find `Products> Enterprise Applications> SSL Certificate` and click to enter. Then click `Buy Now` to enter the certificate purchase page. Here we choose the free version domain name. If there are other requirements, you can choose another domain name.

![](/docs/images/CloudMigrationTencentCloudSSLBuying.png)

Click `Free Quick Application` to enter the application page, fill in the domain name you purchased and your email.

![](/docs/images/CloudMigrationTencentCloudSSLApply.png)

Then perform domain name authentication. If it is a domain name purchased from Tencent Cloud, automatic DNS verification is supported; if not, you need to manually add DNS resolution verification.

![](/docs/images/CloudMigrationTencentCloudSSLApplyVerify.png)

### <a id="ssl-aliyun"></a>Aliyun
To be perfected……

## <a id="ba"></a>Domain name registration
### <a id="ba-tencent-cloud">Tencent Cloud

At present, Tencent Cloud's web-side filing is being upgraded and only supports the use of small programs for filing. You can scan the small program code below for website filing step by step. The filing review will take a long time, and the review will be completed within one month after submission.

<img src="https://imgcache.qq.com/open_proj/proj_qcloud_v2/mc_2014/beian/new/css/img/beian-img-info.png" style="width: 200px">

### <a id="ba-aliyun-">Aliyun

## <a id="connect-server"></a>Connect to the server

The server can use the `ssh` protocol to connect remotely, and different systems use different tools.

### Connect to the server on Windows

Since Windows versions before Win10 did not have built-in OpenSSH, additional connection tools are required to connect to the server. There are many types of tools, such as `XShell`, `PuTTY`, etc. The usage is basically the same. You can search for the usage method.

When connecting, fill in the server's public IP in the Host Name (Host Name or IP Address) column, the port is generally the default `22`, the user name is generally `root`, and the password is the one we purchased in the previous section After the server reset the password, and then connect to be able to enter the server terminal interface.

### Connect to the server on MacOS or Linux

In macOS and Linux, we only need to open the terminal (Terminal), use the `ssh` command to connect to the server, as follows (Win10 can also use the same command to connect in CMD).

```sh
ssh root@${IP host} -p ${port}
```

For example, to connect to a server with a public IP of `1.2.3.4`, the port used by `ssh` is `3366`.

```sh
ssh root@1.2.3.4 -p 3366
```

After pressing Enter, enter the password to enter the server terminal and perform operations such as TARS framework installation, application development, and deployment.