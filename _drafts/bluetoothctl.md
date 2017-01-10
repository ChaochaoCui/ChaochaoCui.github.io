#bluetoothctl分析

bluetoothctl采用Client和Server的架构，和bluetoothd通信。其中bluetoothctl为Client，bluetoothd为Server。

bluetoothctl作为Client，自己缓存了一份所有设备的信息，包括本地蓝牙设备，和远端蓝牙设备。
在程序刚开始的时候，通过调用dbus_message_new_method_call(“org.bluez",
						"/",
						”org.freedesktop.DBus.ObjectManager",
						"GetManagedObjects");来获取已有设备的所有信息，之后通过"org.bluez"的InterfacesAdded和InterfacesRemoved这两个消息来动态的更新设备的信息，包括新设备的添加，和已有设备的删除。
						
						
	client->added_watch = g_dbus_add_signal_watch(connection, service,
						client->root_path,
						DBUS_INTERFACE_OBJECT_MANAGER,
						"InterfacesAdded",
						interfaces_added,
						client, NULL);
	client->removed_watch = g_dbus_add_signal_watch(connection, service,
						client->root_path,
						DBUS_INTERFACE_OBJECT_MANAGER,
						"InterfacesRemoved",
						interfaces_removed,
						client, NULL);

这两个函数就是bluetoothctl用来处理bluetoothd发过来的InterfacesAdded和InterfacesRemoved的两个消息。
bluetoothctl就是通过来实现设备的管理的。