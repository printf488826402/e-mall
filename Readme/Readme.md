# 停止mysql服务
systemctl stop mysqld

# 卸载mysql相关包
yum remove -y mysql* mariadb*

# 删除数据和配置（可选）

rm -rf /var/lib/mysql
rm -rf /etc/my.cnf

然后创建一个通用网络：

同一个网络下的容器可以直接用 **容器名互相通信**，不需要记 IP。

网络和外部隔离，避免容器 IP 冲突。

可以配合 `--network hm-net` 在 `docker run` 时指定容器加入这个网络。

```Bash
docker network create hm-net
```

使用下面的命令来安装MySQL：

```Bash
docker run -d \
  --name mysql \
  -p 3306:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  -v /root/mysql/data:/var/lib/mysql \
  -v /root/mysql/conf:/etc/mysql/conf.d \
  -v /root/mysql/init:/docker-entrypoint-initdb.d \
  --network hm-net\
  mysql
```

此时，通过命令查看mysql容器：

```Bash
docker ps
```
![Clip_2025-08-19_21-39-00.png](Clip_2025-08-19_21-39-00.png)![img.png](../img.png)
![Clip_2025-08-19_21-36-50](C:\Users\liuyang\AppData\Local\Programs\PixPin\Temp\Clip_2025-08-19_21-36-50.png)

![img.png](img.png)
在虚拟机中分别输入：
docker build -t hmall .
(查看docker相关配置信息)
docker images
docker ps

docker run -d --name hm -p 8080:8080 --network hm-net hmall
(查看docker日志)