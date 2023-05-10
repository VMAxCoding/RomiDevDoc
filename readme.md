# Romi Robot Kit (for FIRST) 快速入门指南

### —— by [GitHub@Mehver|这水怎么没味儿啊](https://github.com/Mehver)

# 1 简介

### 1.1 Pololu

Pololu 是一个教学&DIY电路硬件器材供应商，类似国内的矽递科技。他们把一些常用的开发板和教学电路等组件产品化，提供给业余开发者和学生。也算是创客教育的一类。

- Pololu 官网: https://www.pololu.com/
- Pololu GitHub: https://github.com/pololu
- 矽递科技官网: https://www.seeedstudio.com/
- 矽递科技 GitHub: https://github.com/Seeed-Studio/

### 1.2 Romi

Romi 是 Pololu 的产品。Pololu 作为 FIRST 竞赛中的第三方，其产品 Romi 也只是部分还原了 FIRST 竞赛套件的开发流。因此在下文中学习和理解 Romi 的时候，建议把它当做一个**机器人开发套件**而不是 **FIRST 机器人开发套件**，以提醒这两者间的独立性。

- Romi官方详情: https://www.pololu.com/product/4022
- Romi主板官方详情: https://www.pololu.com/product/3544
- 开发文档: https://www.pololu.com/docs/0J69
- FRC版开发文档: https://docs.wpilib.org/en/stable/docs/romi-robot/index.html

#### 1.2.1 学Romi的理由

**Romi 作为一个简易版的机器人，可以帮助小白快速掌握硬件编程和开发。**

Romi 和 FIRST 机器人在代码层面存在可复用性，但都在基础层面。这就类似于，学习了伪代码后，会发现各编程语言的基本逻辑是相同的。因此 Romi 确实适合从未接触过硬件编程的人用来入门 FIRST 竞赛的软件开发。但对于已经有过 Arduino 等单片机开发经验的人来说，学习 Romi 对 FIRST 竞赛帮助有限。

#### 1.2.2 不学Romi的理由

**哪怕是不同的 FIRST 竞赛之间，其技术流程也存在较大的差异。这注定了 Romi 套件和 FIRST 竞赛间仍存在较大的独立性。**

就像 `1.2.1` 中说的，如果你已经入门了单片机和编程，或者你希望专注于 FIRST 竞赛的硬件部分，Romi 并不能教会你什么。由于 Romi 是一个来自第三方的开发套件，其自由度远大于 FIRST 竞赛，后者需要的更多是对官方指定硬件的熟悉。更何况，FIRST 竞赛在机械工程方面的难度和发挥空间更是 Romi 所不具备的。

#### 1.2.3 本文立场

本文将着重于明晰 Romi 开发平台本身的概念，而不是侧重于 FIRST 竞赛相关的模拟。**如果仅为使 Romi 模拟FRC机器人，可以参看官方文档，按步骤操作即可，并不需要过度学习该平台的技术细节。**

因此，综合 `1.2.1` 和 `1.2.2` 所述，**如果你的目标是参加 FIRST 竞赛，请自行考虑是否应该学习本文。**

## 2 上手

### 2.1 知识储备

在继续阅读本文之前，有一些硬件开发的基础知识需要了解。此处将罗列必要的相关概念，以及推荐的学习资料。请在进入下一步之前了解相关概念。

#### 2.1.1 基本的计算机知识

**此项非必须，但可以大大降低后续学习时的抽象度。**

时间充裕的话，建议先了解计算机结构以及基本的编程原理。建议可以先从基础的软件编程入手。或者动手组装一台电脑，了解CPU、内存等结构的作用。

- 【强烈推荐】《计算机速成课 [40集全/精校] - Crash Course Computer Science》B站: https://www.bilibili.com/video/BV1EW411u7th

**注: 如果你是万科梅沙书院VMA的学生，可以选择 CSE202 / CSE302 / CSE304 (2022) 的课程学习 `2.1.1` 的相关概念*

#### 2.1.2 Arduino / 单片机开发板

<u>**Arduino**</u> 是目前最流行的<u>**单片机开发平台**</u>，其中包含 **<u>Arduino 开发板</u>**、**<u>Arduino 固件</u>**、**<u>Arduino 编译器</u>**等。

- 【推荐】《Arduino极速入门教程——两篇文章让你会用Arduino（上）》CSDN: https://yunwuhai.blog.csdn.net/article/details/113528255
- 【推荐】《Arduino极速入门教程——两篇文章让你会用Arduino（下）》CSDN: https://yunwuhai.blog.csdn.net/article/details/113558575
- 《Arduino IDE使用教程-超详细》CSDN: https://blog.csdn.net/as480133937/article/details/105331315

- 《单片机开发板》百度百科: https://baike.baidu.com/item/%E5%8D%95%E7%89%87%E6%9C%BA%E5%BC%80%E5%8F%91%E6%9D%BF

**注: 如果你是万科梅沙书院VMA的学生，可以选择 EGR309 (2022) 的课程学习 `2.1.2` 的相关概念*

#### 2.1.3 树莓派 / Linux 开发板

**<u>树莓派</u>**是目前最流行的 <u>**Linux on ARM 开发平台**</u>。其级别从微波炉都在用的单片机，升级到了手机级别的ARM处理器。从运行 Arduino 固件，升级到了 Linux 系统。但其本质都是运行程序。此处不用过多的学习，但至少需要会给树莓派安装操作系统，并且配置开发环境。

- 【推荐】《第一课：什么是树莓派》CSDN: https://blog.csdn.net/qq_27320195/article/details/105215305
- 【推荐】《第二课：基于树莓派的10个经典项目(树莓派能做什么)》CSDN: https://blog.csdn.net/qq_27320195/article/details/105444549
- 【推荐】《第三课：购买您的第一个树莓派》CSDN: https://blog.csdn.net/qq_27320195/article/details/108877481
- 【推荐】《树莓派折腾指南之系统安装及远程登陆（无头安装、无显示器系统安装）》CSDN: https://blog.csdn.net/suool/article/details/105218395
- 《树莓派如何完全无头(无屏无网线无键盘鼠标)安装》CSDN: https://blog.csdn.net/weixin_34321753/article/details/88986145
- 《Linux 教程》RUNOOB: https://www.runoob.com/linux/linux-tutorial.html
- 《Linux基本指令》博客园: https://www.cnblogs.com/xiaxiangming/p/15096542.html

### 2.2 准备 Romi

Romi Robot Kit for FIRST 小车可以被拆分为车底盘部分以及树莓派开发板。其中，不带树莓派的底盘本身就是一块 Arduino 主板，熟悉 Arduino 的人看到 Romi 32U4 时 就能马上想到 Arduino UNO R3 使用的单片机 ATMEGA328PU4。而树莓派在 Romi 的运行中并不是必需品，但是是作为上位机，通过 I²C 提供更复杂的控制。

因此，不需要树莓派做上位机，Romi 也能作为一个 Arduino 机器人正常的运行。而安装树莓派后则可以进行更复杂的控制，甚至模拟 FIRST 的开发环境。

**如果仅为模拟 FIRST 竞赛的环境，可以直接参看下方的开发文档。而本文会提供非FRC版，更全面的配置介绍。**

- 开发文档: https://www.pololu.com/docs/0J69
- FRC版开发文档: https://docs.wpilib.org/en/stable/docs/romi-robot/index.html
- Romi Robot Kit for FIRST: https://www.pololu.com/product/4022
- Romi 32U4 Control Board: https://www.pololu.com/product/3544
- Romi包库开发文档: https://pololu.github.io/romi-32u4-arduino-library/
- 【推荐】Romi + 树莓派4B文档 (非官方): https://github.com/czbeatty/FRC-Romi-Programming-Course/tree/main/Lessons
- Romi + 树莓派4B示范视频 (非官方): https://www.youtube.com/watch?v=mop51tpWWcA

#### 2.2.1 硬件组装

直接参看官方文档:

- 开发文档-硬件组装: https://www.pololu.com/docs/0J69/4
- FRC版开发文档-硬件组装: https://docs.wpilib.org/en/stable/docs/romi-robot/hardware.html

#### 2.2.2 Romi 32U4 Control Board 底盘 (主板) Arduino 部分

##### 2.2.2.1 Arduino IDE 配置

安装 Arduino IDE:

- 【推荐】《Arduino极速入门教程——两篇文章让你会用Arduino（上）》CSDN: https://yunwuhai.blog.csdn.net/article/details/113528255
- 【推荐】《Arduino极速入门教程——两篇文章让你会用Arduino（下）》CSDN: https://yunwuhai.blog.csdn.net/article/details/113558575
- 《Arduino IDE使用教程-超详细》CSDN: https://blog.csdn.net/as480133937/article/details/105331315

直接参看官方文档:

- 开发文档-ArduinoIDE: https://www.pololu.com/docs/0J69/5.2
- 库管理器安装 `Pololu A-Star Boards`

测试代码:

```c++
/*
  Blink

  Turns an LED on for one second, then off for one second, repeatedly.

  Most Arduinos have an on-board LED you can control. On the UNO, MEGA and ZERO
  it is attached to digital pin 13, on MKR1000 on pin 6. LED_BUILTIN is set to
  the correct LED pin independent of which board is used.
  If you want to know what pin the on-board LED is connected to on your Arduino
  model, check the Technical Specs of your board at:
  https://www.arduino.cc/en/Main/Products

  modified 8 May 2014
  by Scott Fitzgerald
  modified 2 Sep 2016
  by Arturo Guadalupi
  modified 8 Sep 2016
  by Colby Newman

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink
*/

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

###### 2.2.2.1.1 Arduino IDE 安装错误和不识别问题排查

- 《arduino usb串口驱动_Arduino开发环境的搭建与编程入门基础教程》CSDN: https://blog.csdn.net/weixin_39844590/article/details/111197427

- 《arduino usb串口驱动_正确安装驱动的姿势》CSDN: https://blog.csdn.net/weixin_39734399/article/details/111205281

##### 2.2.2.2 Arduino IDE 使用 Romi 32U4 包库

直接参看官方文档:

- 开发文档-ArduinoIDE 使用 Romi 库: https://www.pololu.com/docs/0J69/6
- 库管理器安装 `Romi32U4`
- Romi包库开发文档: https://pololu.github.io/romi-32u4-arduino-library/

测试代码:

```c++
/*
  2022.5.14 new file
  This example code is written by:
  https://github.com/SynthesisDu
*/

#include <Romi32U4.h>

Romi32U4Motors motors;
Romi32U4ButtonA buttonA;

void setup()
{
  // Wait for the user to press button A.
  buttonA.waitForButton();
  // Delay so that the robot does not move away while the user is
  // still touching it.
  delay(1000);
}

void loop()
{
  // Run forward.
  ledYellow(1);
  for (int speed = 0; speed <= 400; speed++)
  {
    motors.setLeftSpeed(speed);
    motors.setRightSpeed(speed);
    delay(2);
  }
  for (int speed = 400; speed >= 0; speed--)
  {
    motors.setLeftSpeed(speed);
    motors.setRightSpeed(speed);
    delay(2);
  }

  // Run backward.
  ledYellow(0);
  for (int speed = 0; speed >= -400; speed--)
  {
    motors.setLeftSpeed(speed);
    motors.setRightSpeed(speed);
    delay(2);
  }
  for (int speed = -400; speed <= 0; speed++)
  {
    motors.setLeftSpeed(speed);
    motors.setRightSpeed(speed);
    delay(2);
  }

  delay(500);
}
```

##### 2.2.2.3 Romi 32U4 Control Board 底盘配置为下位机

使用树莓派控制 Arduino 下位机时使用 I²C 信号传输，此时 Arduino 需要烧录专门的程序用以接收上位机的控制。

**FRC版不需要此步骤，其定制版树莓派系统会自行烧录程序，跟随FRC版文档即可。**

直接参看官方文档: 

- 开发文档-I²C 信号规范: https://www.pololu.com/docs/0J69/3.7
- 开发文档-将 Arduino 配置为下位机: https://www.pololu.com/blog/577/building-a-raspberry-pi-robot-with-the-a-star-32u4-robot-controller
- 官方包库-Romi 32U4 下位机包库: https://github.com/pololu/pololu-rpi-slave-arduino-library

#### 2.2.3 树莓派上位机部分

##### 2.2.3.1 树莓派系统安装

FRC版系统安装教程:

- FRC版开发文档-树莓派系统安装: https://docs.wpilib.org/en/stable/docs/romi-robot/imaging-romi.html

普通系统安装教程:

- 《树莓派折腾指南之系统安装及远程登陆（无头安装、无显示器系统安装）》CSDN: https://blog.csdn.net/suool/article/details/105218395
- 《树莓派如何完全无头(无屏无网线无键盘鼠标)安装》CSDN: https://blog.csdn.net/weixin_34321753/article/details/88986145

###### 2.2.3.1.1 系统安装的错误排查

- **系统盘烧录不成功**

  1. 如果教程中使用的软件无法排故，可以尝试 Rufus，我目前用过最强大的系统烧录软件。市面上有和没有的系统，家用主板到服务器我基本都试过，没遇到过 Rufus 造成的问题。
     - Rufus 发布页: https://rufus.ie/zh/
     - Rufus 微软商城版: https://apps.microsoft.com/store/detail/rufus/9PC3H3V7Q9CH
     - Rufus GitHub: https://github.com/pbatard/rufus

  2. 如果 Rufus 无法解决，接下来考虑下载的系统镜像不完整，尝试重新下载或更换镜像。
  3. 如果还有问题，基本可以怀疑是硬件的问题，可以尝试更换读卡器、更换SD/TF卡。因为这类存储卡转接USB也依靠一个桥主控芯片，便宜货确实容易有兼容性问题。

- **系统盘不引导**
  1. 如果新烧录的系统盘无法运行树莓派系统，直接重试一遍烧录系统的步骤。
  2. 上一步无效的话尝试以其他文件格式格式化存储介质。例如切换 GPT/MBR 分区表，修改 NTFS/FAT32 文件系统。
  3. 如果依然不行，换个系统镜像试试，否则为硬件问题。其实第二步和第三步概率相近，基本不分先后。
  4. 此处硬件问题就比较杂了，如果缺乏经验，也没什么好的建议了。

##### 2.2.3.2 连接树莓派

此处多提一嘴，如果使用树莓派4B等有无线网卡的型号，是可以直接连接树莓派的 WiFi 的。不同版本的操作系统可能有不同的 WiFi 密码，可以在 GitHub 下载的位置查看。

###### 2.2.3.2.1 首次启动故障排查

- **通电红灯常亮，绿灯不亮**
  按理说刚通电时，红灯常亮，绿灯会闪烁。红灯表示通电，绿灯表示读盘。绿灯闪烁说明树莓派开始加载操作系统了。而我本人就遇到通电后绿灯完全不亮的情况。
  - 我的排查结果是 Romi 提供的供电不足，树莓派无法开机。在更换电池前我直接给树莓派外接了 TypeC 的充电器，直接正常开机。
  - 后续扒掉外接线，更换电池，同样正常开机。
  - 此故障的原因大概是化学电池的电压波动超限，其电压依然能够点亮 Romi 的 LED 但无法让树莓派开机。

## 3 使用

### 3.1 FIRST 开发模式

#### 3.1.1 安装软件开发环境

安装 WPILib 模组版 VSCode，之后便可和其他 FIRST 机器人一样在 VSCode 中开发。

- 官方安装包 GitHub 下载: https://github.com/wpilibsuite/allwpilib/releases

##### 3.1.1.1 Windows 系统

Windows 版本的安装包以 .iso 文件的形式打包。安装的部分可以参考这个视频:

- Romi + 树莓派4B示范视频 (非官方): https://www.youtube.com/watch?v=mop51tpWWcA

###### 3.1.1.1.1 Windows 安装注意事项

- 直接用压缩软件解压此 .iso 文件可能会提示文件损坏，其实无需解压，只需要右键文件 --> 打开方式 --> 文件资源管理器，直接运行安装程序即可。
- 运行安装程序后，偶尔会有命令行窗口弹出。
- 建议在能访问外网的网络环境下安装。
- 有 VPN 的情况下，包含在线下载，总安装时常一般不超过10分钟。

##### 3.1.1.2 Linux 系统

Linux 版本的安装包以 .tar.gz 文件的形式打包。

##### 3.1.1.3 MacOS 系统

MacOS 版本的安装包以 .dmg 文件的形式打包。

### 3.2 Arduino 开发模式

直接参看官方文档:

- 开发文档-ArduinoIDE 使用 Romi 库: https://www.pololu.com/docs/0J69/6
- Romi包库开发文档: https://pololu.github.io/romi-32u4-arduino-library/

### 3.3 树莓派 -- I²C -> Arduino 开发模式

直接参看官方文档:

- 开发文档-I²C 信号规范: https://www.pololu.com/docs/0J69/3.7
- 开发文档-将 Arduino 配置为下位机: https://www.pololu.com/blog/577/building-a-raspberry-pi-robot-with-the-a-star-32u4-robot-controller
- 官方包库-Romi 32U4 下位机包库: https://github.com/pololu/pololu-rpi-slave-arduino-library
