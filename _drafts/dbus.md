http://www.ibm.com/developerworks/cn/linux/l-dbus.html

http://blog.csdn.net/eastmoon502136/article/details/10044993

#DBus Message Types
###DBUS_MESSAGE_TYPE_INVALID	0
###DBUS_MESSAGE_TYPE_METHOD_CALL 1
###DBUS_MESSAGE_TYPE_METHOD_RETURN	2
###DBUS_MESSAGE_TYPE_ERROR	3
###DBUS_MESSAGE_TYPE_SIGNAL	4


Address = dbus_bus_get
[Bus Name] = dbus_bus_request_name
	Path
		Interface
			Method
			
			
each message has a header, including fields  and 