---
{"dg-publish":true,"permalink":"/0-class-notes/linux/","dgPassFrontmatter":true,"created":"2023-10-10T09:27:40.635+08:00"}
---

```
systemctl restart 服务名称 //开机自启动
systemctl status  服务名称 //查看服务状态
systemctl start   服务名称 //启动服务
systemctl restart 服务名称 //重新启动
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

#### 用户权限
`u` 表示文件的所有者 (user)
`g` 表示文件的所属组 (group)
`o` 表示其他用户 (others)
`a` 表示所有用户 (all)

`4` 表示读权限 (read)
`2` 表示写权限 (write)
`1` 表示执行权限 (execute)

`7` 表示读、写、执行权限 (4 + 2 + 1)
`6` 表示读、写权限 (4 + 2)
`5` 表示读、执行权限 (4 + 1)

```shell
-rw-r--r-- 1 root root 0 10月 17 11:20 file.txt
$ chmod +100 file.txt      //给所有者添加执行权限
```
