# linux-4.10
linux 4.10 source for my n3160 board


# 更新日志：

2017.3.13  <br>
测试GPIO驱动。 <br>

加载：<br>
modprobe gpio_f7188x <br>

用户空间测试： <br>
echo 80 > /sys/class/gpio/export <br>
echo "out" > /sys/class/gpio/gpio80/direction # 此时默认是0电平 <br>
echo 1 > /sys/class/gpio/gpio80/value <br>
echo 80 > /sys/class/gpio/unexport <br>
（注：主板使用super io芯片f81866扩展，4.10内核支持。加载gpio_f7188x驱动，主板上共80~87可用，适用于GPIO子框架） <br>


2017.3.14 <br>
修改iTCO看门狗驱动。 <br>
编译： <br>
make modules SUBDIRS=drivers/watchdog <br>
加载: <br>
insmod drivers/watchdog/iTCO_vendor_support.ko <br>
insmod drivers/watchdog/iTCO_wdt.ko <br>

测试： <br>
echo 1 > /sys/bus/platform/drivers/iTCO_wdt/iTCO_wdt.0.auto/wdt_enable <br>
(注：4.10版本与3.17版本路径上有不同) <br>

