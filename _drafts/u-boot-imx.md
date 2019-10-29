front: 前部分
rear: 后部分

_start: (arch/arm/lib/vectors.S)
reset (arch/arm/cpu/armv7/start.S)
cpu_init_cp15 (arch/arm/cpu/armv7/start.S)
cpu_init_crit (arch/arm/cpu/armv7/start.S)
	lowlevel_init (arch/arm/cpu/armv7/lowlevel_init.S)
		s_init (arch/arm/mach-imx/mx6/soc.c)
_main (arch/arm/lib/crt0.S)
	board_init_f_alloc_reserve (common/init/board_init.c)
	board_init_f_init_reserve (common/init/board_init.c)
	board_init_f (common/board_f.c)
	
	relocate_code (arch/arm/lib/relocate.S)
	relocate_vectors (arch/arm/lib/relocate.S)
	
	c_runtime_cpu_setup d
	board_init_r (common/board_r.c)
		main_loop 
	