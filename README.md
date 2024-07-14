# 服务器环境工具包（centos）
## /java
自行下载JDK8*.tar.gz包，并放在./java/目录下，推荐JDK版本为1.8.0_202，执行命令：
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

# 设置阿里源
sudo yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

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


