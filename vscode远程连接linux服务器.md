### 配置连接到局域网或者同一个网络上的linux服务器
1，Windows生成密钥对参考 https://www.cnblogs.com/sinicheveen/p/14203670.html
2，将密钥对配置到linux ~/ssh目录中，如果没有.ssh文件使用“ssh localhost”生成
如果没有authorized_keys，则手动创建将秘钥复制过去
3，配置vscocde ssh插件注意各种信息不要写错特别是ip地址和user，要与虚拟机一致。
4，如果上述都没有问题，尝试在“网络配置管理中-->禁用VMNET8/VMNET1”-->然后启用，我禁用我重启VMNet8