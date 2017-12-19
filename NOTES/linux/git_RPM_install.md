## git RPM安装

### RPM包下载

#### git下载地址为:`ftp://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/git-1.8.3.1-11.el7.x86_64.rpm`

```
#下载git
wget -c ftp://rpmfind.net/linux/centos/7.4.1708/os/x86_64/Packages/git-1.8.3.1-11.el7.x86_64.rpm

#下载perl,perl-Error,perl-Git,perl-TermReadKey
wget -c http://mirror.centos.org/centos/7/os/x86_64/Packages/perl-5.16.3-292.el7.x86_64.rpmwget -c http://mirror.centos.org/centos/7/os/x86_64/Packages/perl-Error-0.17020-2.el7.noarch.rpm
wget -c http://mirror.centos.org/centos/7/os/x86_64/Packages/perl-Git-1.8.3.1-11.el7.noarch.rpm
wget -c http://mirror.centos.org/centos/7/os/x86_64/Packages/perl-TermReadKey-2.30-20.el7.x86_64.rpm

#安装依赖包及git
rpm -ivh perl-Error-0.17020-2.el7.noarch.rpm 
rpm -ivh perl-TermReadKey-2.30-20.el7.x86_64.rpm
rpm -ivh perl-Git-1.8.3.1-11.el7.noarch.rpm  git-1.8.3.1-11.el7.x86_64.rpm --force --nodeps


```



#### gitlab-runner安装

```
#安装及下载
wget -c https://packages.gitlab.com/runner/gitlab-runner/packages/fedora/25/gitlab-runner-10.1.0-1.x86_64.rpm/download
rpm -ivh download
```

