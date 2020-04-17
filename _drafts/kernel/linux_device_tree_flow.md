start_kernel() --- init/main.c
	setup_arch(&command_line)  --arch/arm/kernel/setup.c
   		unflatten_device_tree() -- drivers/of/fdt.c
   		   initial_boot_params
   		   of_root 
