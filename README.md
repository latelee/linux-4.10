# linux-4.10
linux 4.10 source for my n3160 board

log：
2017.3.13
测试GPIO驱动。

加载：
# modprobe gpio_f7188x

用户空间测试：
# echo 80 > /sys/class/gpio/export
# echo "out" > /sys/class/gpio/gpio80/direction # 此时默认是0电平
# echo 1 > /sys/class/gpio/gpio80/value
# echo 80 > /sys/class/gpio/unexport
（注：主板使用super io芯片f81866扩展，4.10内核支持。加载gpio_f7188x驱动，主板上共80~87可用，适用于GPIO子框架）

------------------------------------------------------------


2017.3.14
修改iTCO看门狗驱动。
编译：
make modules SUBDIRS=drivers/watchdog
加载:
insmod drivers/watchdog/iTCO_vendor_support.ko
insmod drivers/watchdog/iTCO_wdt.ko

测试：
echo 1 > /sys/bus/platform/drivers/iTCO_wdt/iTCO_wdt.0.auto/wdt_enable
(注：4.10版本与3.17版本路径上有不同)
------------------------------------------------------------
