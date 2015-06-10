# What is this spec?

[Nginx](http://nginx.org) with [headers-more-module](http://wiki.nginx.org/NginxHttpHeadersMoreModule)

# How to build SRPM and RPM?

You can build SRPM and RPM with headers-more-module using the official SRPM.

You need to install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/).


### Update nginx.spec.centos7.patch and nginx.spec.centos7.patch

please edit to Version, Release, and changelog
if new module exist, please edit to new version

You refer to changelog of nginx.spec.
In order to edit the changelog of nginx.spec.centos7.patch and nginx.spec.centos7.patch

```
$ curl -LO http://nginx.org/packages/centos/6/SRPMS/nginx-1.8.0-1.el7.ngx.src.rpm
$ rpm -Uvh nginx-1.8.0-1.el7.ngx.src.rpm
$ cd ~/rpmbuild/SPECS
$ ls
nginx.spec
```

(example)[https://github.com/feedforce/nginx-headers-more-rpm/blob/master/nginx.spec.centos6.patch]


### CentOS7

```
$ vagrant up centos7
$ vagrant ssh centos7
$ sudo yum update -y
$ sudo yum install -y rpm-build gcc
$ curl -LO http://nginx.org/packages/centos/7/SRPMS/nginx-1.8.0-1.el7.ngx.src.rpm
$ rpm -Uvh nginx-1.8.0-1.el7.ngx.src.rpm
$ cd ~/rpmbuild/SOURCES
$ curl -L -o headers-more-nginx-module-0.26.tar.gz https://github.com/openresty/headers-more-nginx-module/archive/v0.26.tar.gz
$ cd ~/rpmbuild/SPECS
$ patch -p0 < /vagrant/nginx.spec.centos7.patch
$ rpmbuild -ba nginx.spec
エラー: ビルド依存性の失敗:
openssl-devel >= 1.0.1 は nginx-1:1.8.0-ff1.el7.centos.ngx.x86_64 に必要とされています
zlib-devel は nginx-1:1.8.0-ff1.el7.centos.ngx.x86_64 に必要とされています
pcre-devel は nginx-1:1.8.0-ff1.el7.centos.ngx.x86_64 に必要とされています
$ sudo yum install -y openssl-devel zlib-devel pcre-devel
$ rpmbuild -ba nginx.spec
(省略)
書き込み完了: /home/vagrant/rpmbuild/SRPMS/nginx-1.8.0-ff1.el7.centos.ngx.src.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/nginx-1.8.0-ff1.el7.centos.ngx.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/nginx-debug-1.8.0-ff1.el7.centos.ngx.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/nginx-debuginfo-1.8.0-ff1.el7.centos.ngx.x86_64.rpm
```

### CentOS6

```
$ vagrant up centos6
$ vagrant ssh centos6
$ sudo yum update -y
$ sudo yum install -y rpm-build gcc
$ curl -LO http://nginx.org/packages/centos/6/SRPMS/nginx-1.8.0-1.el6.ngx.src.rpm
$ rpm -Uvh nginx-1.8.0-1.el6.ngx.src.rpm
$ cd ~/rpmbuild/SOURCES
$ curl -L -o headers-more-nginx-module-0.26.tar.gz https://github.com/openresty/headers-more-nginx-module/archive/v0.26.tar.gz
$ cd ~/rpmbuild/SPECS
$ patch -p0 < /vagrant/nginx.spec.centos6.patch
$ rpmbuild -ba nginx.spec
エラー: ビルド依存性の失敗:
openssl-devel >= 1.0.1 は nginx-1.8.0-ff1.el6.ngx.x86_64 に必要とされています
zlib-devel は nginx-1.8.0-ff1.el6.ngx.x86_64 に必要とされています
pcre-devel は nginx-1.8.0-ff1.el6.ngx.x86_64 に必要とされています
$ sudo yum install -y openssl-devel zlib-devel pcre-devel
$ rpmbuild -ba nginx.spec
(省略)
き込み完了: /home/vagrant/rpmbuild/SRPMS/nginx-1.8.0-ff1.el6.ngx.src.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/nginx-1.8.0-ff1.el6.ngx.x86_64.rpm
書き込み完了: /home/vagrant/rpmbuild/RPMS/x86_64/nginx-debug-1.8.0-ff1.el6.ngx.x86_64.rpm
```
