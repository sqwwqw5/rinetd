使用[@linhua](https://github.com/linhua55/lkl_study)的黑科技rinetd为OVZ构架的VPS开启bbr
***
Debian 8 64 步骤:
#### 下载rintd二进制文件(原版bbr和修改版bbr二选一即可):
    1. wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd
    2. wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd_bbr_powered -O /root/rinetd
  * 修改权限:
`chmod +x rinetd`
#### 修改rinetd的配置文件rinetd.conf,添加监听地址:
`vi rinetd.conf`
```
# bindadress bindport connectaddress connectport
0.0.0.0 443 0.0.0.0 443
0.0.0.0 80 0.0.0.0 80
```
#### 设置开机启动
`vi /etc/systemd/system/rinetd.service`
```
[Unit]
Description=rinetd

[Service]
ExecStart=/root/rinetd -f -c /root/rinetd.conf raw venet0:0
Restart=always
  
[Install]
WantedBy=multi-user.target
```
#### 最后执行:
`systemctl enable rinetd.service && systemctl start rinetd.service`  
***
##### LKL BBR RINETD
For more details:[linhua55/lkl_study](https://github.com/linhua55/lkl_study)
