# Vmware Workstation



VMware Workstation Pro 14.1.0 注册码：

```
激活密钥：
AU5WA-0EF9M-0811P-REP5X-ZFK9A
ZV382-6VX96-H81LP-1ZZG9-PVKF4
GU34A-41G4Q-H88CY-3WPNT-XUK8F

CG54H-D8D0H-H8DHY-C6X7X-N2KG6
ZC3WK-AFXEK-488JP-A7MQX-XL8YF
AC5XK-0ZD4H-088HP-9NQZV-ZG2R4
ZC5XK-A6E0M-080XQ-04ZZG-YF08D
ZY5H0-D3Y8K-M89EZ-AYPEG-MYUA8
```





### 虚拟网卡



本机和虚拟机进行通信，

如果本机和虚拟机之间无法通信，可以选择：

- 修改当前虚拟网卡的类型（通信模式）

- 切换虚拟网卡
- 新建一个虚拟网卡



**新建一个仅主机模式的虚拟网卡：** 

查看虚拟主机的ip，这里假设是：`192.168.66.166`

打开`虚拟网络编辑器 > 添加网络 > 设置为仅主机模式 > 子网掩码：192.168.66.0 > 子网掩码： 255.255.255.0 > 配置某个虚拟机使用该网卡 > 测试连接 > 如果连接失败，查看主机网络适配器，找到刚才新建的 VMware Network Adapter Vm.. > 查看属性 > 找到internet协议版本4 > 属性 > 手动为其设置 ip 地址为192.168.66.**网段的值`   



新建一个NAT模式的虚拟网卡：



