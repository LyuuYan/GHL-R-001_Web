# GHL-R-001_Web
歌华链固件，可能适用于newwifi3（存疑）本人第一次编译的固件，难免会有多多少少问题（指的是插件太多太臃肿了QAQ），请各位大佬见谅，接下来介绍固件用途
# 用途
适用于锐捷校园网，实现多设备防检测（内置UA2F），本人测试地点位于龙院，校园网是web认证。宿舍总共7人，已经用了一星期暂未出现断线问题，其他学校暂未作测试，仅供参考！
# 注意事项
1.ua2f并不是开机自启的，如果学校有断电的话需要手动启动。
2.无线问题也是同上。
# 解决办法
1.可以通过winscp连接路由器，进入这个目录
/etc/config/ua2f
修改ua2f内容，将里面的'0'都改为'1'即可开启开机自启。
2.创建本地脚本start_wifi
内容为
#!/bin/sh /etc/rc.common
START=99
start() {
  ip link set ra0 up
  ip link set rai0 up

  brctl addif br-lan ra0
  brctl addif br-lan rai0
}
放到 /etc/init.d/ 然后执行 chmod 755 /etc/init.d/start_wifi && /etc/init.d/start_wifi enable && /etc/init.d/start_wifi start
# 插件合集概括
状态：负载均衡、TTYD终端  
服务：V2RAY服务器、广告屏蔽大师PLUS+、ShadowSocksR Plus+、解除网易云音乐播放限制、WIFI计划、KMS服务器、Frp内网穿透、MWAN3分流助手
网络存储：FTP服务器、Aria2配置  
VPN：ZEroTier
网络：Turbo ACC网络加速、多线多拨、负载均衡、带宽监控
主题：opentop
# 关于个人遇到校园网叠加网速&自动连接校园网的问题
当初我的想法很天真，想把宿舍的3个宽带叠加后再通过wifi共享给整间宿舍，解决办法是设置3个WAN口（VLAN），后来发现设置以后只能关闭其中两个wan口后另一个wan口插入网线才能跳出校园网认证网页，如果3个wan口同时开就不能。也就是说如果想实现3个wan口同时叠加并且有效的话需要手动重复关闭、开启wan口操作才行，属实麻烦。。本人还是小白暂且放弃。。
自动连接校园网暂时没还研究出来，感兴趣的具体可参考此网站
