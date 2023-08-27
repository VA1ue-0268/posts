---
title: C遍历读取结构体成员（位域）
date: 2022-11-05 00:53:43
tags:
---

实验课上遇到的题，简化流水灯代码  
代码如下：
```c
led_ctrl.led1 = 1; //给第一个LED(led1)的状态赋值为1，将LED状态设置为“亮”
led_ctrl_data(1,led_ctrl); //发送每个灯的状态至功能模块
task_delay(50);//延时500ms,即led1会保持点亮状态500ms
led_ctrl.led1 = 0;
led_ctrl_data(1,led_ctrl);

led_ctrl.led2 = 1; //给第二个LED(led2)的状态赋值为1，将LED状态设置为“亮”
led_ctrl_data(1,led_ctrl);
task_delay(50);
led_ctrl.led2 = 0;
led_ctrl_data(1,led_ctrl);
...
```
一共有8个冗余的代码块  
**led_ctrl_t** 结构体为：
```c
typedef struct
{
  uint8_t led1:1;
  uint8_t led2:1;
  uint8_t led3:1;
  uint8_t led4:1;
  uint8_t led5:1;
  uint8_t led6:1;
  uint8_t led7:1;
  uint8_t led8:1;
} led_ctrl_t;
```
一开始想的是传统方法
```c
led_ctrl_t led;
uint8_t *p = &led;
int i;
for(i=0; i<sizeof(led_ctrl_t)/sizeof(uint8_t); i++)
{
    (*p++) = i+1;
    ...
}
```
但发现使用了位域的数据结构（课上没学一开始还不知道），又刚好是8位，那就简单了，流水灯直接使用移位运算不就好了  
最后简化为：
```c
led_ctrl_t *p_m = &led_ctrl;
uint8_t i;
uint8_t *p = (uint8_t*)p_m;
*p = 1;
for(i=0; i<8; i++)
{
    led_ctrl_data(1,led_ctrl);
    *p <<= 1;
    task_delay(50);
}
```
就这调试了几十分钟，最终用10行代码替代了原来三四十行，特此记录一下。