# Call the Interface of Service

[中文版](/docs/HowToUseRPC.md)

In [Create the first Tars application](/docs/QuickStart_en.md), we created our first Tars application `FirstApp`, which contains the service `HelloServer`, and added an interface `hello`.

Next, let's create a service and call the `hello` interface. Here we also take TarsCpp as an example.

* [Create Service](#create-server)
* [Import tars file](#refer-tars-file)
* [Call Interface](#rpc)
* [Deploy Service](#server-deploy)

## <a id="create=-server"></a>Create Service

For a more intuitive display, we create an Http service and use the script `cmake_http_server.sh` in TarsCpp to create the project.

```sh
sh /usr/local/tars/cpp/script/cmake_http_server.sh FirstApp HttpServer Http
```

It will create the following file.

```sh
.
└── HttpServer
    ├── build
    ├── CMakeLists.txt          # cmake file
    └── src
        ├── HttpServer.h       # service implement
        ├── HttpServer.cpp
        ├── HttpImp.h          # hello interface implement class
        ├── HttpImp.cpp
        └── CMakeLists.txt
```

It can be found that unlike creating the tars service, the tars interface file is not generated because the service uses the http protocol instead of the tars protocol.

## <a id="refer-tars-file"></a>Import tars file

Since this service needs to call the interface of `HelloServer`, we need to import the tars interface file of `HelloServer`.

We copy `Hello.tars` to this directory, and then convert it to the corresponding C++ file `Hello.h`.

```sh
/usr/local/tars/cpp/tools/tars2cpp Hello.tars
```

The final project directory is as follows

```
.
└── HttpServer
    ├── build
    ├── CMakeLists.txt         # cmake file
    └── src
        ├── HttpServer.h       # service implement
        ├── HttpServer.cpp
        ├── Hello.tars
        ├── HttpImp.h          # hello interface implement class
        ├── HttpImp.cpp
        └── CMakeLists.txt
```

## <a id="rpc"></a>Call Interface
### Get communicator
Services that use the tars protocol communicate through a communicator. When the service is started, a communicator object needs to be obtained. Through the communicator, a proxy for a specific service is generated, and the service or client can use the proxy to call the interface of the specific service.

In the service, the communicator can be obtained through `Application::getCommunicator()`.

### Generate proxy
First, we include `Hello.h` in `HttpImp.h` and add the variable `_pHello` of the proxy class of the server `Hello`, as follows

#### HttpImp.h
```cpp
#ifndef _HttpImp_H_
#define _HttpImp_H_

#include "servant/Application.h"
#include "Hello.h"

class HttpImp : public Servant
{
public:
    virtual ~HttpImp() {}

    virtual void initialize();

    virtual void destroy();

    int doRequest(TarsCurrentPtr current, vector<char> buffer);

private:
    int doRequest(const TC_HttpRequest &req, TC_HttpResponse &rsp);
    FirstApp::HelloPrx _pHello;
};
/////////////////////////////////////////////////////
#endif
```


Then, get the communicator in `initialize()` of `HttpImp.cpp`, and use the communicator to initialize the proxy object, as follows

```cpp
...

void HttpImp::initialize()
{
    _pHello = Application::getCommunicator()->stringToProxy<FirstApp::HelloPrx>("FirstApp.HelloServer.HelloObj");
}

...
```

### Call interface through proxy
We can find two `doRequest` functions in `HttpImp.cpp`, they are

```cpp
int HttpImp::doRequest(TarsCurrentPtr current, vector<char> &buffer)
```

and

```cpp
int HttpImp::doRequest(const TC_HttpRequest &req, TC_HttpResponse &rsp)
```

The former is a function that needs to be defined when the service uses a non-TARS protocol. This has been defined for us here, so we don't need to modify it.

The latter is the specific logic of Http service, so we add interface calling logic here, as follows

```cpp
int HttpImp::doRequest(const TC_HttpRequest &req, TC_HttpResponse &rsp)
{
    string msg = "Hello Tars!";
    /**调用hello接口***/
    string helloMsg;
    int ret = _pHello->hello(helloMsg);
    if (ret == 0)
    {
        msg += "<br>" + helloMsg;
    }
    /****************/
    rsp.setContentType("html/text");
    rsp.setResponse(msg.c_str(), msg.size());
    return 0;
}
```

The part added in the middle is the logic of calling the `hello` interface. The function of the `if` statement is to add the returned string `helloMsg` to the output `msg` if there is no error in calling the service (returns 0).

At the same time, you need to modify the `html/text` in `rsp.setContentType("html/text")` to `text/html`. The script automatically generated is wrong, and if it is not modified, the browser will download the page directly.

The modified `HttpImp.cpp` is as follows

```cpp
#include "HttpImp.h"
#include "servant/Application.h"

using namespace std;

//////////////////////////////////////////////////////
void HttpImp::initialize()
{
    _pHello = Application::getCommunicator()->stringToProxy<FirstApp::HelloPrx>("FirstApp.HelloServer.HelloObj");
}

//////////////////////////////////////////////////////
void HttpImp::destroy()
{
}

int HttpImp::doRequest(TarsCurrentPtr current, vector<char> &buffer)
{
    TC_HttpRequest req;
    TC_HttpResponse rsp;
    // parse request header
    vector<char> v = current->getRequestBuffer();
    string sBuf;
    sBuf.assign(&v[0], v.size());
    req.decode(sBuf);

    int ret = doRequest(req, rsp);

    rsp.encode(buffer);

    return ret;
}

int HttpImp::doRequest(const TC_HttpRequest &req, TC_HttpResponse &rsp)
{
    string msg = "Hello Tars!";
    /**调用hello接口***/
    string helloMsg;
    int ret = _pHello->hello(helloMsg);
    if (ret == 0)
    {
        msg += "<br>" + helloMsg;
    }
    /****************/
    rsp.setContentType("text/html");
    rsp.setResponse(msg.c_str(), msg.size());
    return 0;
}
```

At this point, we have completed the code to call the `hello` interface of the `HelloServer` service, and then compile the project and package it

```sh
cd build
cmake ..
make
make tar
```

## <a id="server-deploy"></a>Publish Service

If the process of service release is not clear, you can see [Create the first Tars application--service deployment release](/docs/QuickStart_en.md#server-deploy)

First, deploy the service on the TarsWeb management page. The configuration is as follows, where the node IP is your server IP, and the port can be automatically generated by clicking "Get Port", or you can fill in a port that is not occupied by yourself.

![](/docs/images/HowToUseRPCHttpServerDeployConf.png)

Next, download the previously generated release package and publish it to the service.

Finally, open `1.2.3.4:1004` (make sure the port has been opened, Alibaba Cloud needs to add the configuration of the corresponding port in the security group to open), you can see the following page

![](/docs/images/HowToUseRPCHttpServerOutput.png)

The second line shows Hello World, which is the string returned by calling the `hello` interface, indicating that the interface is successfully called.

At this point, we have learned how to call other tars service interfaces under TarsCpp. The calling process of other languages is similar. You can refer to the official documentation.