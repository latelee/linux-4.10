# linux-4.10
linux 4.10 source for my n3160 board


# 更新日志：

2017.3.13  <br>
测试GPIO驱动。 <br>
注：主板使用super io芯片F81866扩展，4.10内核支持。加载gpio_f7188x驱动，主板上共80~87可用，适用于GPIO子框架 <br>
加载：<br>
modprobe gpio_f7188x <br>

用户空间测试： <br>
echo 80 > /sys/class/gpio/export <br>
echo "out" > /sys/class/gpio/gpio80/direction # 此时默认是0电平 <br>
echo 1 > /sys/class/gpio/gpio80/value <br>
echo 80 > /sys/class/gpio/unexport <br>



2017.3.14 <br>
修改intel内部iTCO看门狗驱动。 <br>
手册：搜索TCO_TMR，找到超时时间范围。大约1.2s~613.8s <br>

驱动位置：drivers/watchdog/iTCO_wdt.c <br>
驱动名称：iTCO_wdt.ko <br>

编译： <br>
make modules SUBDIRS=drivers/watchdog <br>
加载: <br>
insmod drivers/watchdog/iTCO_vendor_support.ko <br>
insmod drivers/watchdog/iTCO_wdt.ko <br>

insmod drivers/watchdog/iTCO_wdt.ko start_withtimeout=60 # 指定超时时间为60，此时，wdt会开启 start_withtimeout是修改代码后的 <br>

测试： <br>
echo 1 > /sys/bus/platform/drivers/iTCO_wdt/iTCO_wdt.0.auto/wdt_enable <br>
(注：4.10版本与3.17版本路径上有不同) <br>

2017.3.15 <br>
外部看门狗(F81866)： <br>
超时时间：1秒~255分钟 <br>
f71808e_wdt.ko <br>
文件：drivers/watchdogf71808e_wdt.c <br>
加载： <br>
insmod /lib/modules/4.10.0/kernel/drivers/watchdog/f71808e_wdt.ko  start_withtimeout=60 # 指定超时时间为60，此时，wdt会开启 <br>

