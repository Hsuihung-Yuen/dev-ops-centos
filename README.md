# 服务器环境安装包（CentOS7）
## /java
JDK版本为1.8.0_202，执行命令：
```shell
cd java

# 直接执行安装脚本即可
chmod +x install-java.sh
./install-java.sh

source /etc/profile

java -version

# 卸载jdk
chmod +x remove-java.sh
./remove-java.sh
```

## /maven
maven版本为3.8.8，已配置阿里云镜像
```shell
cd maven

# 直接执行安装脚本即可
chmod +x install-maven.sh
./install-maven.sh

source /etc/profile

mvn --version

# 卸载
chmod +x remove-maven.sh
./remove-maven.sh
```

## Docker
```shell
# 可选
sudo yum -y update

# 卸载旧版本，如果有的话，首次不需要
sudo yum remove docker  docker-common docker-selinux docker-engine

# 安装依赖包
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# 查看docker版本
yum list docker-ce --showduplicates | sort -r

# 这里安装和本机一样的版本，对应后续的compose版本
sudo yum -y install docker-ce-24.0.2

# 启动并设置开机自启
systemctl start docker
systemctl enable docker

# 安装docker-compose，版本为2.18.1
sudo mv ./docker-compose-linux-x86_64 /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# 查看是否成功安装
docker-compose -v
```
### 配置docker 镜像
阿里云提供了镜像源：[https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors(opens new window)](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)- 登录后会获得一个专属的地址
创建daemon.json并设置镜像：
```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxxxxxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```
其他可选配置
```shell
{ "registry-mirrors" : [
    "https://xxxxx.mirror.aliyuncs.com",
    "http://docker.mirrors.ustc.edu.cn",
    "http://hub-mirror.c.163.com"
  ],
  "builder": {
    "gc": {
      "enabled": true,
      "defaultKeepStorage": "20GB"
    }
  },
  "experimental": false,
  "features": {
    "buildkit": true
  }
}

```
一些备选镜像：
```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": [
        "https://dc.j8.work",
        "https://docker.m.daocloud.io",
        "https://dockerproxy.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://docker.nju.edu.cn"
    ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker

```

