# rinetd
在使用@linhua的黑科技rinetd想设置为开机自动运行，google了很久才搞定，做个记录.

步骤:下载rintd二进制文件，配置rinetd.conf，然后执行
vi /etc/init.d/rinetd.sh

#!/bin/sh

### BEGIN INIT INFO
# Provides: rinetd
# Required-Start: $network
# Required-Stop:
# Should-Start:
# Should-Stop:
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: start and stop rinetd
# Description: ovz vps bbr
### END INIT INFO

nohup /root/rinetd -f -c /root/rinetd.conf raw venet0:0 &gt;/dev/null 2&gt;&amp;1 &amp;

最后执行：
chmod +x /etc/init.d/rinetd.sh
cd /etc/init.d
update-rc.d rinetd.sh defaults 97
reboot
