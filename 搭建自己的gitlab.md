# 搭建自己的GitLab

## 准备
* CentOS 6
* Ruby(NodeJS, 之后会使用 Node 来搭建)
* Git
* Redis
* MySQL
* GitLab
* GitLab Shell

## yum
> 为了提高软件安装的速度，当yum源设置为阿里云开源镜像

```
cd /etc/yum.repos.d
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

## 依赖

```
yum -y install libicu-devel patch gcc-c++ readline-devel zlib-devel libffi-devel openssl-devel make autoconf automake libtool bison libxml2-devel libxslt-devel libyaml-devel zlib-devel openssl-devel cpio expat-devel gettext-devel curl-devel perl-ExtUtils-CBuilder perl-ExtUtils-MakeMaker
```

## Git

```
// 查看当前 git 版本
git --version

// 如果小于 1.8 则卸载重新安装
yum remove git
```

## Ruby
```
// 安装 Ruby
mkdir /tmp/ruby && cd  /tmp/ruby
curl --progress ftp://ftp.ruby-lang.org/pub/ruby/ruby-2.1.5.tar.gz | tar xz
cd ruby-2.1.5
./configure --disable-install-rdoc
make && make install

ln -s /usr/local/bin/ruby /usr/bin/ruby
ln -s /usr/local/bin/gem /usr/bin/gem
ln -s /usr/local/bin/bundle /usr/bin/bundle

// 设置ruby gem源为淘宝
gem source -r https://rubygems.org/
gem source -a http://ruby.taobao.org/

gem install bundler --no-ri --no-rdoc
```

## MySQL
自己安装

```
// 创建 gitlabhq_production 库
MySQL> CREATE DATABASE IF NOT EXISTS `gitlabhq_production` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
```

## Redis
```
// 安装 epel, redis 第三方安装源
yum -y install epel-release

// 安装 redis
yum -y install redis

// 判断 redis 是否成功安装
redis-cli

// 启动服务
systemctl start redis.service

// 设置开机启动
systemctl enable redis.service
```

## 未完结
