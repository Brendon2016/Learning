参考[ubuntu16.04使用ipv6](https://blog.csdn.net/scylhy/article/details/72699166)
# 开启ipv6
```
sudo apt-get install miredo
sudo gedit /etc/default/ufw   :将其中的IPV6=no修改为IPV6-yes
sudo invoke-rc.d networking restart
```
# 测试IPV6
- ping6 ipv6.baidu.com
- 浏览器打开ipv6.baidu.com
# 修改hosts文件
```
sudo su
curl https://github.com/lennylxx/ipv6-hosts/raw/master/hosts -L >> /etc/hosts
```

