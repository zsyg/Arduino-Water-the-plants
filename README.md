# Arduino-Water-the-plants
## 一款迷你掌上型的植物浇水系统，包括代码、电路板和适用3D打印的外壳

![](https://github.com/jie326513988/Arduino-Water-the-plants/blob/master/1.jpg)<br>

### 烧录说明<br>
1.将U8g2和MsTimer2的整个文件夹放在你自己的库文件夹里，或者用ArduinoBuilder直接烧录hex文件，暂时还不知道怎样可以一次性把EEPROM和程序一起烧录<br><br>
2.使用ArduinoIDE编译，需要下载两次程序才可以使用<br>
在setup()找到这段程序看说明下载程序<br>
EEPROM.put第一次写入去掉注释，第二次以后注释上<br>
EEPROM.get第一次写入注释上，第二次以后写入去掉注释<br><br>
3.使用ArduinoBuilder烧录也是要烧录两次hex文件，先烧录1，在烧录2。<br><br>
4.必须将arduino pro mini的电源指示LED和LED旁边的限流电阻焊下来，否则电量会很快耗尽，若只焊下LED没焊下电阻就读取电压会烧坏板子！<br><br>
### 原理及功能介绍<br>
1.基本原理，浇水，休眠，唤醒，判断土壤湿度是否达到设置的值，没达到继续休眠，达到就开始浇水，浇到设定的值就休眠，不断循环。比市面上的定时浇水多了一个土壤湿度检测功能，不再是盲目的浇水。<br><br>
2.休眠时电流低至0.8ma，内置750mah锂电池，水泵接口输出电压5v电流800ma，可根据需求选用水泵。<br><br>
3.上电前插上电容式土壤湿度传感器，当然没插也可以开机但会报错。<br>
每次上电需要手动开启浇水功能（主界面第三项），开启浇水功能不代表水泵就会运转，水泵运转要达到浇水下限的值。<br><br>
4.写有传感器和水泵的保护代码，一旦传感器或水泵故障即可触发保护机制，让浇水系统停止工作，并显示故障原因。<br>
传感器保护机制就比较简单，若传感器没工作，读取传感器数值的引脚就会受到干扰，数值会变得非常大，只要判断数值超过一定值就触发保护机制。<br>
水泵保护则是使用水泵超时时间来设定，若输出接口打开，10秒后记录当前的土壤湿度值，过一段时间在将旧的土壤湿度值跟现在的对比,若变化小于5，即会触发保护使浇水系统停止，即可判断水泵没接或水泵没工作或水管没插到土里。<br><br>
### 主要功能<br>
1.浇水上限<br>
2.浇水下限<br>
3.休眠时间设置<br>
4.水泵异常提示<br>
5.传感器异常提示<br>
6.强制关闭传感器<br>
7.清除异常提示<br>
8.手动开启关闭浇水功能<br>
9.水泵超时<br>
10.水泵接口翻转<br>
11.电压校准<br>
12.电池充电时的动画<br>
13.水泵运转时间显示<br>
14.水泵运转时的动画<br>
15.数据断电保存<br><br>
### 引脚定义<br>
6-电机驱动输入引脚1<br>
5-电机驱动输入引脚2<br>
12-传感器电源正极<br>
13-led指示灯（暂时未启用）<br>
2-下按键<br>
3-上按键<br>
4-确认按键<br>
A3-读取电压的引脚<br>
A0-读取土壤湿度的引脚<br>
A2-读取充电状态的引脚<br>
A4-OLED,SDA<br>
A5-OLED,SCL<br>

版本更新说明

    009c
    1.设置界面第二页增加4项的设置
    a.传感器开关
    b.水泵超时
    c.水泵接口翻转
    d.电压校准
    2.修正水泵运转时间显示
    3.主界面下长按按键可调节亮度
    4.优化一些代码逻辑

    008c
    1.因硬件问题移除水泵PWM输出,改为普通高低电平控制，pwm输出会导致系统卡死
    2.主界面增加电池充电时的动画
    3.主界面增加水泵运转时间显示
    4.主界面增加水泵运转时的动画
