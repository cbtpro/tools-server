<!--
 Copyright 2021 peter
 
 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at
 
     http://www.apache.org/licenses/LICENSE-2.0
 
 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

## 开发环境
要求使用以下node版本,
```shell
$ node -v
v14.17.3
$ npm -v
7.x.x
```

```shell
# 全局安装yarn
# 安装依赖
tools/server$ npm install
tools/client$ npm install

# 安装docker

## 配置镜像地址

https://www.runoob.com/docker/docker-mirror-acceleration.html

# 使用docker安装mysql8
```shell
# 拉取最新版本mysql
~/$ docker pull mysql:latest
# 查看本地镜像
~/$ docker images
# 运行容器,但是使用命令中包含密码,请勿在生产环境中使用
~/$ docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root用户密码 mysql
# 查看正在运行的docker容器
~/$ docker ps
# CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              
# PORTS                               NAMES
# a0b984d422a1        mysql               "docker-entrypoint.sh"   5 days ago          Up 2 hours          0.0.0.0:3306->3306/tcp, 33060/tcp   mysql-test

# 停止运行的docker `docker stop CONTAINER ID`
~/$ docker stop a0b984d422a1
# 或者 `docker stop NAMES`
~/$ docker stop mysql-test
# 同理,启动docker也可以用这两种方式
~/$ docker start mysql-test
```

# docker安装mongo

```shell
~/$ docker pull mongo:latest
~/$ docker images 
~/$ docker run -itd --name mongo-test -p 27017:27017 mongo --auth
~/$ docker exec -it mongo mongo admin
# 创建一个名为 admin，密码为 123456 的用户。

>  db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'},"readWriteAnyDatabase"]});
# 尝试使用上面创建的用户信息进行连接。
> db.auth('admin', '123456')
# 退出mongo
> exit
```
参考 https://www.runoob.com/docker/docker-install-mongodb.html

# 使用docker安装redis

```shell
~/$ docker search redis
~/$ docker search redis
~/$ docker pull redis:latest
~/$ docker run -itd --name redis-no-auth -p 6379:6379 redis
# 进入redis容器
docker exec -it redis-no-auth /bin/bash
# 运行redis-cli
root@ef300a6836b0:/data# redis-cli
# 退出redis
127.0.0.1:6379> exit
```

参考 https://www.runoob.com/docker/docker-install-redis.html


# 运行程序
tools/server$ npm run start:dev
tools／client$ npm run start
```