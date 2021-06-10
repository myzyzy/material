# Docker的常用命令
**帮助命令**  
```
docker version	    #显示docker的版本信息 
docker info         #显示docker的系统信息
docker 命令 --help  #帮助命令
```
Docker 的官网文档命令  
**镜像命令**  
docker images 查看所有本地的主机上的镜像
```
root@OpenWrt:~# docker images
REPOSITORY                  TAG       IMAGE ID       CREATED       SIZE
oldiy/music-player-docker   latest    f060773d86e0   2 years ago   81.7MB

#  解释
REPOSITORY  镜像的仓库源
TAG         镜像的标签
IMAGE ID    镜像的ID
CREATED     镜像的创建时间
SIZE        镜像大小
```
docker search   搜索镜像 
```
root@OpenWrt:~# docker search mysql
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   10607     [OK]
mariadb                           MariaDB Server is a high performing open sou…   3977      [OK]
#可选项,通过收藏数来过滤
root@OpenWrt:~# docker search mysql --filter=stars=1000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   10607     [OK]
mariadb   MariaDB Server is a high performing open sou…   3977      [OK]
#列出收藏数大于1000的镜像
```
docker pulll 拉取镜像
```
# 不加任何参数,默认拉取最新
root@OpenWrt:~# docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
# 指定版本下载,,,,拉取mysql的5.6版本


root@OpenWrt:~# docker pull mysql:5.6
5.6: Pulling from library/mysql
a4feded82f54: Pull complete
c1d0e80dd947: Pull complete
a3eb306f0583: Pull complete
9fafb9660ba0: Pull complete
64aef7d42843: Pull complete
488408f75e55: Pull complete
5c154cf95ff0: Pull complete
ae9d479e9699: Pull complete
89e036f05e2f: Pull complete
681eef5c7bd9: Pull complete
1604d620cec0: Pull complete
Digest: sha256:f3515b6a6502d872d5a37db78e4d225c0fcbf8da65d1faf8ce4609c92e2cbaf0
Status: Downloaded newer image for mysql:5.6
docker.io/library/mysql:5.6
```
删除镜像
```
root@OpenWrt:~# docker rmi -f 镜像id        #删除指定镜像
root@OpenWrt:~# docker rmi -f $(docker images -qa)  #删除所有镜像
```
**容器命令**  
*基本理解：* 镜像运行起来的时候叫做容器，第一次运行镜像的时候要指定参数，有容器没有镜像也能运行。<br/>
说明：有镜像才能创建容器，先下载一个centos练手  
 `root@OpenWrt:~# docker pull centos`  
 新建容器并启动
 ```
 docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
 # 参数说明
 --name     #容器名字
 -d         #后台运行
 -i         #交互式操作
 -t         #终端
 -P         #指定容器端口   8080:8080(主机端口:容器端口)

 # 启动并进入容器
 root@OpenWrt:~# docker run -it centos /bin/bash
 #查看容器
 root@OpenWrt:~# docker ps      
 #查看正在运行的容器
-a      显示所有容器
-n=?    显示最近创建的容器
-q      仅显示容器的id号
 ```
退出容器
```
exit        #直接停止并退出
ctrl+P+Q    #容器不停止退出
```
删除容器
```
docker rm 容器id    #不能删除正在运行的容器，加参数-f,强制删除
```
启动和停止容器的操作<br/>
`docker start 容器id`<br/>
`docker stop 容器id`<br/>
`docker restart 容器id`<br/>
`docker kill 容器id`#暴力删除容器  
**常用的其他命令**
