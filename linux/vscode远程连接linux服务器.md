### 配置连接到局域网或者同一个网络上的linux服务器

1，Windows生成密钥对参考 https://www.cnblogs.com/sinicheveen/p/14203670.html
2，将密钥对配置到linux ~/ssh目录中，如果没有.ssh文件使用“ssh localhost”生成
如果没有authorized_keys，则手动创建将秘钥复制过去
3，配置vscocde ssh插件注意各种信息不要写错特别是ip地址和user，要与虚拟机一致。
4，如果上述都没有问题，尝试在“网络配置管理中-->禁用VMNET8/VMNET1”-->然后启用，我禁用我重启VMNet8

vscode无法远程连接机器（虚拟机），本质上是ssh无法连接，所以用ssh如果用ssh可以连接上了，则vscode也可以连接上。

首先考虑连接目标机是否可以ping通，然后看是否可以连上，最后看端口是否打开，一般来所ssh不要求同一网段。

[参考连接]([ssh无法连接本地虚拟机的解决办法 - 星罗棋布 - 梦想之路 (dreams-true.com)](https://www.dreams-true.com/lxqb/2250.html#:~:text=ssh%E6%97%A0%E6%B3%95%E9%93%BE%E6%8E%A5%E8%99%9A%E6%8B%9F%E6%9C%BA%E7%9A%84%E8%A7%A3%E5%86%B3%E5%8A%9E%E6%B3%95%EF%BC%9A,1%E3%80%81%E9%A6%96%E5%85%88%EF%BC%8C%E6%88%91%E4%BB%AC%E8%A6%81%E7%A1%AE%E8%AE%A4%E4%B8%80%E4%B8%8B%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%92%8C%E6%9C%AC%E5%9C%B0%E7%94%B5%E8%84%91%E8%83%BD%E4%B8%8D%E8%83%BDping%E9%80%9A%EF%BC%8C%E5%A6%82%E6%9E%9C%E4%B8%8D%E8%83%BDping%E9%80%9A%E7%9A%84%E8%AF%9D%E5%A4%A7%E6%A6%82%E7%8E%87%E6%98%AF%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE%E5%8E%9F%E5%9B%A0%EF%BC%8C%E8%BF%99%E4%B8%AA%E8%AF%B7%E5%A4%A7%E5%AE%B6%E8%87%AA%E8%A1%8C%E6%90%9C%E7%B4%A2%E8%A7%A3%E5%86%B3%E3%80%82%202%E3%80%81%E6%8E%92%E9%99%A4%E7%AC%AC%E4%B8%80%E7%82%B9%E4%BB%A5%E5%90%8E%EF%BC%8C%E9%82%A3%E4%B9%88%E5%A4%A7%E6%A6%82%E7%8E%87%E5%B0%B1%E6%98%AF%E8%99%9A%E6%8B%9F%E6%9C%BA%E6%B2%A1%E6%9C%89%E5%AE%89%E8%A3%85ssh%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%EF%BC%8C%E6%88%91%E4%BB%AC%E5%8F%AF%E4%BB%A5%E5%9C%A8%E8%99%9A%E6%8B%9F%E6%9C%BA%E4%B8%8A%E8%BE%93%E5%85%A5%EF%BC%9A))


