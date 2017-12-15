# kubernetes-v1.8.1-install-scripts centos7.2
1、基础准备工作
在所有的master、node节点上执行如下操作，关闭防火墙、swap、设置selinx、安装docker、网络组件
(1)关闭防火墙
[root@production-k8s-master zts_api]# setenforce 0
[root@production-k8s-master zts_api]# sed -i s/SELINUX=enable/SELINUX=disable/g /etc/selinux/config 
(2)关闭swap交换分区
[root@production-k8s-master zts_api]# swapoff -a
[root@production-k8s-master zts_api]# cat /etc/fstab 

# 注释掉该文件中的swap分区
# /etc/fstab
# Created by anaconda on Fri Nov 25 05:04:43 2016
#
/dev/mapper/centos-root /                       xfs     defaults        0 0
UUID=8eddcf74-915d-4f74-a72b-05188ce8fbd7 /boot                   xfs     defaults        0 0
#/dev/mapper/centos-swap swap                    swap    defaults        0 0
(3)安装docker、网络组件
[root@production-k8s-master zts_api]# yum install -y docker ebtables socat
[root@production-k8s-master zts_api]# systemctl enable docker && systemctl start docker
(4)添加各节点的hosts解析
[root@production-k8s-master zts_api]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
X.X.X.X production-k8s-master
2、将相关镜像上传到master节点、并分发到node节点
(1)镜像下载地址
百度云盘链接: https://pan.baidu.com/s/1dEOhL2D 密码: anea
(2)将镜像上传到master、node节点上
3、脚本安装
(1)解压缩安装包
[root@production-k8s-master test1]# tar xvf kube-offline-install.tar.gz
[root@production-k8s-master test1]# cd kubeadm/
(2)执行安装脚本
[root@production-k8s-master kubeadm]# sh init-master.sh
（如果master节点，去掉--skip-preflight-checks）









