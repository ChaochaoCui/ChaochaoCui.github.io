#build and install bluez-5.43 on ubuntu 16.04

##配置bluez
./configure --enable-maintainer-mode \
           --enable-debug \
          --prefix=/opt/bluetooth \
          --mandir=/opt/bluetooth/man \
          --sysconfdir=/opt/bluetooth/etc \
          --localstatedir=/var \
          --enable-manpages \
          --enable-backtrace \
          --enable-experimental \
          --enable-nfc \
          --enable-health \
          --enable-sixaxis \
          --disable-datafiles $*
为了不和系统中的bluez5.37相冲突，修改了bluez的安装路經。
其中禁止了SAP profile,因为PC上不支持SIM卡，同时禁止了android平台的应用和服务。
##编译和安装
make && make install
之后会在/opt/bluetooth下看到生成bluez。

##替换系统的bluetoothd进程

用systemctl stop bluetooth停止bluetoothd守护进程失败，原因还没有找到，对systemctl中Service还不是太了解，只能先修改Service，来强制替换系统中的bluetoothd。

用systemctl edit bluetooth 会生成/etc/systemd/system/bluetooth.service.d/override.conf文件，这个文件用来“drop-in"覆盖/lib/systemd/system/bluetooth.service中的配置，override.conf的内容如下：
[Service]
ExecStart=
ExecStart=/opt/bluetooth/libexec/bluetooth/bluetoothd

然后执行systemctl daemon-reload 来加载我们刚才修改的配置。

##看看log
通过查看syslog，我们看到
####bluetoothd[30759]: Bluetooth daemon 5.43
说明我们已经安装bluez-5.43成功了。


问题：
使用systemctl stop bluetooth为什么不能停止bluetoothd运行，通过查看syslog发现bluetoothd确实停止运行，但又立马重启了。
