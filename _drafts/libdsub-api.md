DBusDispatchStatus
指示输入数据的状态
DBUS_DISPATCH_DATA_REMAINS 可能有更多的数据需要被转换成message
DBUS_DISPATCH_COMPLETE 所用可用的数据已经被处理了
DBUS_DISPATCH_NEED_MEMORY 继续转换需要更多的内存




函数文档:
dbus_tool_t dbus_connection_add_filter(DBusConnection* connection,
                                                                  DBusHandleMessageFunction function,
                                                                  void* user_data,
                                                                  DBusFreeFunction free_data_function)
                                                                  
函数说明:
增加message过滤器。
过滤器被用来处理 all incomming messages, 优先于使用dbus_connection_register_object_path()注册的处理。过滤器按照它们被添加的顺序依次执行，同一个
过滤器可以被多次添加，这时过滤器会被多次使用。