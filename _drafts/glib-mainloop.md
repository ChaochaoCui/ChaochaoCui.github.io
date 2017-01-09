\#include <glib.h\>

描述：
 	mainEventLoop为Glib和GTK+管理所有可能的事件源（source of event），这些事件源有很多不同的类型，例如：文件描述符（普通文件，管道，套接字）和超时事件。可以用g_source_attach()来增加事件源。
 	为了允许多个独立的事件源集合可以在不同的线程中使用，每个事件源可以和GMainContext联系在一起。一个GMainContext只能运行在单个线程里，但是其它线程中的事件源可以被added(removed)到这个GMainContext。
 	每个事件源会被分配一个优先级（priority）。默认的priority是G_PRIORITY_DEFAULT 0。小于0说明拥有更高的优先级。大于0说明拥有更低的优先级。优先级高的事件会被优先处理。
 	idle functions可以被添加到mainEventLoop中，同时分配一个priority。当没有更高优先级的事件，这些idle functions会被运行。
 	
    GMainLoop类型代表一个主事件循环（main event loop）。用g_main_loop_new()来创建一个GMainLoop实例。增加过事件源后，执行g_main_loop_run()。 mainEventLoop会一直检测注册的事件源，和分发它们。最后，其中一个事件源的处理过程会调用g_main_lloop_quit()来结束mainLoop，g_main_loop()将返回。
   允许递归的创建GMainLoop实例。GTK+应用经常出现这种情况，例如：主程序中现实一个模态的对话框。Note that event sources are associated with a particular GMainContext, and will be checked and dispatched for all main loops associated with that GMainContext.
   
   GTK+包含了这些函数中的封装。
   
####创建新的事件类型 
   GMainLoop最特殊的功能是可以创建新的事件类型。新的事件类型通过继承GSource来实现，新实现的事件类型的结构体（struct）必须把GSource作为第一个元素，其它的元素确定了新事件类型的功能。为了创建一个新事件类型实例，call g_source_new() passing in the size of the derived structure and a table of functions. These GSourceFuncs determine the behavior of the new source type.
