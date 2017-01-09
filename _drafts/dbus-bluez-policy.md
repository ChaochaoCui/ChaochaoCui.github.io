#		使用libdbus访问org.bluez的policy问题

使用libdbus创建一个"com.ts.music"connection, 然后调用org.bluez的Methods时出现如下error:
####Connection to Session D-Bus
####Request Name ErrorDBusError.name:org.freedesktop.DBus.Error.AccessDenied
####DBusError.message: Connection ":1.2507" is not allowed to own the service ####"com.ts.music" due to security policies in the configuration file

根据信息Error.AccessDenied可推测是没有访问权限，从http://stackoverflow.com/questions/11170118/dbus-systembus-policies可知，可简单的修改dbus的配置文件/etc/dbus-1/systemd.conf:
#<policy>

    	<allow own="org.testobj.service"/>
</policy>
			
然后重启dbus: systemctl reload dbus
再执行程序即可。