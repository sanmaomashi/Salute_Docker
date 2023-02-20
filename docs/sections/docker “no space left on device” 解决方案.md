问题原因：出现此问题一般是 docker 根目录空间不足导致

解决方案：修改 Docker Root Dir 的值，指向一个更大空间的目录.

## 1.查看docker磁盘使用情况

```bash
docker system df
```

查看docker挂载目录

```bash
docker info  | grep "Docker Root Dir"
```

默认目录为/var/lib/docker

## 2.查看目录的占用情况

```bash
df -hl /var/lib/docker
```

## 3. 关闭docker

```vbnet
systemctl stop docker
```

## 4. 创建新的挂载目录

```bash
mkdir -p /app/dockerdata
```

## 5. 复制数据复制数据

```bash
mv /var/lib/docker /app/dockerdata/
```

## 6.修改docker配置文件

```shell
vim /lib/systemd/system/docker.service
# 修改ExecStart=/usr/bin/dockerd-current下行后面加
--graph /app/dockerdata/docker
```

## 7.重启docker

```bash
systemctl disable docker
systemctl enable docker
systemctl daemon-reload
systemctl start docker
```

## 8.查看挂载目录

```bash
docker info  | grep "Docker Root Dir"
```

## 9.修改完成

