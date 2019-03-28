#Linux Pinctl and GPIO
	struct chip_gpio;
		const char *gpiochip_is_requested(struct gpio_chip*chip,unsigned offset);
		int gpiochip_add_data_with_key(struct gpio_chip *chip, void *data, struct lock_class_key *lock_key, struct lock_class_key *request_key);  --- gpiochip_add_data(chip, data) 
	struct gpio_device
	struct gpio_desc;
	struct gpio_pin_range;