### **docker构建漏洞测试环境遇到的坑**

###### 1.安装docker

https://docs.docker.com/install/linux/docker-ce/centos/

可以使用链接中的脚本安装方法（推荐）

```
docker -v   #有版本信息表示安装成功
```



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

*# Compile (optional)* 	构建（下载镜像，这步容易因为网络出问题）
docker-compose build 

*# Run* 	启动
docker-compose up -d   



###### 其他：

1.build未完成，然后重新build出错？

因为你build一次了，如果你想要重新build，可以执行

```
docker-compose build --no-cache
```

build完了就启动即可

```
docker-compose up
```

2.当docker-compose up -d后，如果修改了yml文件，譬如将某个service的port更改后，想要重新创建docker container，那么可以通过下面的命令

```
docker-compose up -d --force-recreate
```

