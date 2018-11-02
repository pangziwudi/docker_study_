### 如何安装docker在ubuntu
>不要直接安装docker，如果没有配置源成功，很可能会造成必要的困难。 


###### 1.卸载旧版本 
```shell 
    sudo apt-get remove docker \
                 docker-engine \ 
                 docker.io

```

###### 2.在ubuntu14.04中需要安装可选内核模块，在ubuntu 16.04+以上不需配置 

```shell 
    sudo apt-get update 
    sudo apt-get upgrade 
    
    sudo apt-get install \
            linux-image-extra-$(uname -r)\ 
            linux-image-extra-virtual 

```

###### 3.使用apt安装docker 
由于apt源使用https以确保软件下载过程中不被篡改，我们需要首先添加使用https传输的软件包以及ca证书。 

```shell 
    sudo apt-get install update 

    sudo apt-get install \
                 apt-transport-https \ 
                 ca-certificates \ 
            curl \
            software-properties-common 
``` 
鉴于国内网络原因，建议使用国内源，官方源见注释中查看。 

为了确认所下载的软件包的合法性，需要添加软件源的GPG密钥。 

```shell 
    curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
    #官方源 
    # curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 
``` 
然后我们需要向`source.list`中添加Docker软件源 

```shell 

$ sudo add-apt-repository \
    "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
    $(lsb_release -cs) \
    stable"


# 官方源
# $ sudo add-apt-repository \
#    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
#    $(lsb_release -cs) \
#    stable"

``` 
>以上命令会添加稳定版本的 Docker CE APT 镜像源，如果需要最新或者测试版本的 Docker CE 请将 stable 改为 edge 或者 test。从 Docker 17.06 开始，edge test 版本的 APT 镜像源也会包含稳定版本的 Docker。


###### 4.开始安装docker CE 
更新apt软件包缓存，并安装docker-ce： 
```shell 
    sudo apt-get update 

    sudo apt-get install docker-ce 
``` 

###### 5.使用脚本安装docker  
在测试或者开发环境中Docker官方为了简化流程，提供了一套
简便的安装脚本，ubuntu系统上可以使用这套脚本安装： 

```shell 
    $ curl -fsSL get.docker.com -o get-docker.sh
    $ sudo sh get-docker.sh --mirror Aliyun
``` 
执行完这个命令之后，脚本会自动的将一切准备工作做好，并且把docker ce的Edge版本安装在系统中。  

###### 6.测试docker是否安装正确 

```shell 
    docker run hello-world 

    Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
ca4f61b1923c: Pull complete
Digest: sha256:be0cd392e45be79ffeffa6b05338b98ebb16c87b255f48e297ec7f98e123905c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

``` 
若能正确输出上诉信息，则安装docker 成功。

###### 镜像加速 
鉴于国内网络的问题，后续拉取镜像十分缓慢，强烈建议安装Docker之后配置，国内镜像加速。 


###### 参考文档 
[Docker官方安装文档](https://docs.docker.com/install/linux/docker-ce/ubuntu/)


