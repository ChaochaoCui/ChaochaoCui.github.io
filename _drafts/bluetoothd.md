bluetoothd:
main:
	adapter_init();
		mgmt_master  = mgmt_new_default();
						io_set_read_handler(mgmt->io, can_read_data, mgmt, NULL);