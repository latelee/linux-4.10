# linux-4.10
linux 4.10 source for my n3160 board


# 更新日志：

2017.3.13
测试GPIO驱动。
注：主板使用super io芯片F81866扩展，4.10内核支持。加载gpio_f7188x驱动，主板上共80~87可用，适用于GPIO子框架
加载：
modprobe gpio_f7188x

用户空间测试：
echo 80 > /sys/class/gpio/export
echo "out" > /sys/class/gpio/gpio80/direction # 此时默认是0电平
echo 1 > /sys/class/gpio/gpio80/value
echo 80 > /sys/class/gpio/unexport



2017.3.14/15
修改intel内部iTCO看门狗驱动。
手册：搜索TCO_TMR，找到超时时间范围。大约1.2s~613.8s

驱动位置：drivers/watchdog/iTCO_wdt.c
驱动名称：iTCO_wdt.ko

编译：
make modules SUBDIRS=drivers/watchdog
加载:
insmod drivers/watchdog/iTCO_vendor_support.ko
insmod drivers/watchdog/iTCO_wdt.ko

insmod drivers/watchdog/iTCO_wdt.ko start_withtimeout=60 # 指定超时时间为60，此时，wdt会开启 start_withtimeout是修改代码后的

测试：
echo 1 > /sys/bus/platform/drivers/iTCO_wdt/iTCO_wdt.0.auto/wdt_enable
(注：4.10版本与3.17版本路径上有不同)

2017.3.15
外部看门狗(F81866)：
超时时间：1秒~255分钟(注：最大超时值为255，但可配置单位是分钟或秒)
f71808e_wdt.ko
文件：drivers/watchdogf71808e_wdt.c
加载：
insmod /lib/modules/4.10.0/kernel/drivers/watchdog/f71808e_wdt.ko  start_withtimeout=60 # 指定超时时间为60，此时，wdt会开启

