# enging 的安装文档
## centos 6
本文档在 centos 6.5 上测试通过
### 前期准备
#### 更新系统所有组件到最新的版本
```bash
# yum upgrade -y
```

#### 设置网络
在配置 vdsm 的时候, 需要本机有一个名为 ovirtmgmt 的桥接网络, 不然会报以下错误:
```bash
2014-01-14 18:25:00,587 ERROR [org.ovirt.engine.core.bll.SetNonOperationalVdsCommand] (DefaultQuartzScheduler_Worker-30) [7118faa8] Host local_host is set to Non-Operational, it is missing the following networks: ovirtmgmt
```

在 centos 下设置桥接网络的可以参考[这里](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s2-networkscripts-interfaces_network-bridge.html)

### 安装设置
```bash
# 1. 添加 oVirt 官方源
# yum localinstall http://ovirt.org/releases/ovirt-release-el.noarch.rpm

# 2. 增加 epel 仓库, 下面的命令执行之后, 会在仓库的文件夹下看到 epel 仓库的信息
# yum install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
# ls /etc/yum.repos.d/epel*
# /etc/yum.repos.d/epel.repo  /etc/yum.repos.d/epel-testing.repo

# 3. 安装 ovirt-engine
#yum install -y ovirt-engine

# 4. 安装 all-in-one 插件, 同时配置 engine 为计算节点
# yum install -y ovirt-engine-setup-plugin-allinone

# 5. 设置 ovirt-engine, 有两点需要注意, 其它按照默认就可以了:
# 1) 是否在本机配置 VDSM, 选 yes
# 2) 选择一个合适的密码
# engine-setup

# 6. 打开 http://engine-ip 就可以看到搭建好的环境了
```
