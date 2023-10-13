---
{"dg-publish":true,"permalink":"/0-class-notes/linux/","dgPassFrontmatter":true,"created":"2023-10-10T20:11:34.064+08:00"}
---

```
systemctl restart 服务名称 //开机自启动
systemctl status  服务名称 //查看服务状态
systemctl start   服务名称 //启动服务
systemctl reload  服务名称 //重新加载配置文件（不终止服务）
```

```
journalctl -xe     //查看日志
```

```
//查看防火墙
firewall-cmd --zone=public --list-ports
```

```
vi /etc/redis.conf    //查看redis.conf文件
```
