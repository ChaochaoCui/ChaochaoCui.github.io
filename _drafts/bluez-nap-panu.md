#bluez中NAP和PANU的使用
环境：ubuntu 16.04 
          bluez 5.37运行在ubuntu 16.04上。
          华为android手机，系统版本 android 6.0，使用的蓝牙协议栈为bluedroid。
          
##bluez的PANU
在bluez中使用PANU，使用的客户端软件是bluetooh manager，android手机需要打开蓝牙，并打开《移动网络共享》中的《蓝牙共享网络》，然后在ubuntu中用bluetooth manager连接”network access point“，之后就可以使用电脑通过手机连接外网。
 通过这验证了，bluez中PANU正常和android手机中NAP正常。
 
 ##bluez的NAP
 由于在ubuntu上现成NAP设置的客户端，所以需要编写代码设置一下。在网上找到了https://github.com/ykasidit/ecodroidlink，通过运行这个软件，然后在android手机上通过《设置》《蓝牙》连接oser-thunder（ubuntu上的蓝牙设备名），然后在它的配置项打开《互联网访问》，即可用手机通过电脑访问外网。
 
 
 通过分析ecodroidlink的源代码，ecodroidlink主要做了两个事：
    1:配置本地蓝牙设备，设置agnent（用于配对验证），注册nap Service。
    2:建立bridge。这个bridge用来把电脑本地的网口(eth0或者enp2s0)和手机蓝牙设备所形成的网口进行连接。
    
    