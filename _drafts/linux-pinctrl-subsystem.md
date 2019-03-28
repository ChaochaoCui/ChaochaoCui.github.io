#Linux Pinctrl Subsystem

	#include <linux/pinctrl/pinctrl.h>
	
	struct	 pinctrl_dev *devm_pinctrl_register(struct device *dev, struct pinctrl_desc *pctldesc, void *driver_data);
	
	void	 devm_pinctrl_unregister(struct device*dev, struct pinctrl_dev *pctldev);
该函数对用来创建和注销一个pinctrl device, 其中struct pinctrl_desc的定义如下:
	