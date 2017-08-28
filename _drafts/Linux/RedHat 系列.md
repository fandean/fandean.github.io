
# RedHat 系列系统

查看系统版本：
```shell
cat /etc/redhat-release

# 查看详细信息
cat /etc/*-release
```


## Fedora

[Fedora 22/23升级到 Fedora 24 - Linux大神博客](https://www.linuxdashen.com/upgrade-fedora-23-workstation-fedora-24 "Fedora 22/23升级到 Fedora 24 - Linux大神博客")

```shell
# 查看当前系统版本
cat /etc/redhat-release
Fedora release 23 (Twenty Three)

# 升级原有系统的软件
sudo dnf upgrade --refresh
# 安装升级插件
sudo dnf install dnf-plugin-system-upgrade
# 指定要升级到 fedora 26 
sudo dnf system-upgrade download --releasever=26
```





直接从 Fedora 23 升级到 Fedora 26。出现错误：

```shell
$ sudo dnf system-upgrade download --releasever=26 --allowerasing

总计                                                                                    1.3 MB/s | 1.0 GB     13:21     
警告：/var/lib/dnf/system-upgrade/js-coffee-script-1.10.0-7.fc26.noarch.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID 64dab85d: NOKEY
Curl error (37): Couldn't read a file:// file for file:///etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-i386 [Couldn't open file /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-i386]
下载的软件包保存在缓存中，直到下次成功执行事务。
您可以通过执行 'dnf clean packages' 删除软件包缓存。

```



进入 [软件包签名密钥](https://getfedora.org/keys/ "软件包签名密钥") 网站下载公钥文件，点击对应版本的主要按钮，在弹出的对话框中点击 "Fedora Project"  

```shell
cd /etc/pki/rpm-gpg/

# 下载fedora 26对应的 公钥文件
wget https://getfedora.org/static/64DAB85D.txt

cp 64DAB85D.txt RPM-GPG-KEY-fedora-i386

# 再次运行
sudo dnf system-upgrade download --releasever=26 --allowerasing
```





## CentOS

