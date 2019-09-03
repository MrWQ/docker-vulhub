### **docker构建漏洞测试环境遇到的坑**

###### 1.安装docker

https://docs.docker.com/install/linux/docker-ce/centos/

可以使用链接中的脚本安装方法（推荐）

```
###为了方便直接把安装脚本命令复制过来了
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

```
docker -v   #有版本信息表示安装成功
```

也可以参考这个：

https://vulhub.org/#/docs/install-docker-one-click/



###### 2.安装docker-compose

```
docker-compose -v
```

如果有版本信息，

说明第一步的脚本中已经安装了docker-compose，那么跳过这一步，

如果没有安装，参考链接：

https://vulhub.org/#/docs/install-docker-compose/



###### 3.克隆项目

  *# Download the latest version of the vulhub* 
git clone https://github.com/vulhub/vulhub.git  

*# Entry vulnerability directory*  切换到要用到环境的目录
cd /path/to/vuln/ 

*# Compile (optional)* 	构建，这一步需要用root用户执行，如果不想用root，参考[其他3](#其他：)
docker-compose build 

*# Run* 	启动（下载镜像，这步容易因为网络出问题）
docker-compose up -d   



###### 4.移除环境

前面说了，docker-compose会默认根据当前目录下的配置文件启动容器，在关闭及移除环境的时候，也需要在对应目录下。我们执行`docker-compose up -d`后，不要离开当前目录即可，漏洞测试结束后，执行如下命令移除环境：

```
docker-compose down
```



###### 其他：

1. build未完成，然后重新build出错？


因为你build一次了，如果你想要重新build，可以执行

```
docker-compose build --no-cache
```

build完了就启动即可

```
docker-compose up -d
```

2. 当docker-compose up -d后，如果修改了yml文件，譬如将某个service的port更改后，想要重新创建docker container，那么可以通过下面的命令

```
docker-compose up -d --force-recreate
```

3. 如果您想使用docker作为非根用户，那么现在应该考虑将您的用户添加到“docker”组中:

   ```
     sudo usermod -aG docker your-user
   ```

4. 关机后重新构建和启动的话需要启动docker

   ```
   service docker start
   ```

   还可以设置docker开机自启动：
   
   ```
   systemctl enable docker
   ```