# 单机/伪分布式安装
## 创建用户，并分配sudo权限
sudo useradd -m hadoop -s /bin/bash
sudo passwd hadoop
sudo adduser hadoop sudo
## 免密登录
cd ~/.ssh/                     # 若没有该目录，请先执行一次ssh localhost
ssh-keygen -t rsa              # 会有提示，都按回车就可以
cat ./id_rsa.pub >> ./authorized_keys  # 加入授权

ssh-copy-id hostname   # 将公钥发送到相应主机，实现免密登录

# 分布式安装
## 安装步骤

### 0) 创建hadoop用户
sudo useradd -m hadoop -s /bin/bash
sudo passwd hadoop
sudo adduser hadoop sudo
### 1) ip, 主机名配置和映射 /etc/hosts /etc/hostname
### 2) 关闭防火墙和selinux(centos only)
### 3) 将系统启动级别改为3(即多用户模式，centos only)
### 4) 配置免密登录
cd ~/.ssh/                     # 若没有该目录，请先执行一次ssh localhost
ssh-keygen -t rsa              # 会有提示，都按回车就可以
ssh-copy-id hostname   # 将公钥发送到相应主机，实现免密登录
### 5) 安装jdk
### 6) 时间同步
apt install ntp
ntpdate ntp1.aliyun.com
### 7) 安装hadoop,并配置相关文件(加hadoop文件夹)
### 8) 远程发送到其他主机
### 9) 执行格式化（主节点）
hadoop namenode -format
### 10) 启动(任意节点)
start-dfs.sh
start-yarn.sh
### 11) 网页查看
http://master:50070 (hdfs)
http://master:8088  (yarn)


# HA部署策略
| 主机        | 安装软件      |
| --------:   | -----:   |
| master01        | $1      |
| master02        | $1      |
| slave01        | $1      |
| slave02        | $1      |
| slave03        | $1      |