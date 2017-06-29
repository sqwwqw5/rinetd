使用@linhua的黑科技rinetd为OVZ构架的VPS开启bbr 参考：https://www.v2ex.com/t/353778#r_4311799  
***
Debian 8 64 步骤:  
#### 下载rintd二进制文件(原版bbr和修改版bbr二选一即可):  
* `wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd`  
* `wget --no-check-certificate https://raw.githubusercontent.com/mixool/rinetd/master/rinetd_bbr_powered -O /root/rinetd`  
###### 修改权限:  
`chmod +x rinetd`
#### 修改rinetd的配置文件rinetd.conf,添加监听地址:  
`vi rinetd.conf`  
`# bindadress bindport connectaddress connectport   
0.0.0.0 443 0.0.0.0 443  
0.0.0.0 80 0.0.0.0 80`  
#### 设置开机启动
`vi /etc/systemd/system/rinetd.service`
`[Unit]  
Description=rinetd server  
  
[Service]  
ExecStart=/root/rinetd -f -c /root/rinetd.conf raw venet0:0  
Restart=always  
  
[Install]  
WantedBy=multi-user.target`  
#### 最后执行:  
`systemctl enable rinetd.service && systemctl start rinetd.service`  

PS:记录在这里其实是为了方便自己下载rinetd文件
