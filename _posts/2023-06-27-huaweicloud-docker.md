---
layout: post
date: 2023-06-27
author: Leo
header-img: "img/bg-material.jpg"
permalink: /huaweicloud-docker-20230627/

title: "华为云CentOS7中docker的安装"
category: "programme"
tags: [bigdata, docker]
---

使用华为云耀云服务器CentOS 7.9版本。
# docker安装
参考华为云开源镜像中Docker-CE镜像的配置。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/677815/1687844308856-170e05b6-943a-49fa-a830-5cba7a3e8dc3.png#averageHue=%23fbfafa&clientId=ue5527760-dc35-4&from=paste&height=602&id=ub6f133e0&originHeight=602&originWidth=771&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91581&status=done&style=none&taskId=u25a8ece1-8b98-40ec-9909-54102b4ef69&title=&width=771)

```shell
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

wget -O /etc/yum.repos.d/docker-ce.repo https://repo.huaweicloud.com/docker-ce/linux/centos/docker-ce.repo

sudo sed -i 's+download.docker.com+repo.huaweicloud.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo

sudo yum makecache fast
sudo yum install -y docker-ce

sudo systemctl start docker
```

PS：注意以上命令在CentOS8中有问题，只推荐在CentOS7中使用。
# docker-compse安装
直接从docker-compse在github的项目中下载指定平台和架构的二进制文件。
比如linux平台 x86_64平台。
```shell
curl -L https://github.com/docker/compose/releases/download/v2.19.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

# 华为云docker镜像加速
在华为云中支持docker镜像加速。
登录华为云账号后找到SWR服务后，如下图找到镜像加速器按钮。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/677815/1687844917962-781bd249-9df5-418b-88ec-8e7e39750555.png#averageHue=%23fbfafa&clientId=ue5527760-dc35-4&from=paste&height=733&id=ubd5bbae2&originHeight=733&originWidth=1815&originalType=binary&ratio=1&rotation=0&showTitle=false&size=218460&status=done&style=none&taskId=u3b09cc63-b8d6-4ef7-8035-749677ed2c1&title=&width=1815)
弹出如下配置：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/677815/1687844811632-85b51c6b-2157-4a2c-bd46-ee26db05f36f.png#averageHue=%23fdfefa&clientId=ue5527760-dc35-4&from=paste&height=562&id=ua7bf9ad5&originHeight=562&originWidth=879&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86573&status=done&style=none&taskId=u0429280b-69a6-4bd2-aaee-9e256c4590a&title=&width=879)
配置完成后，重启docker
```shell
sudo systemctl restart docker
```

# 资料

- [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)
- [https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/](https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/)


