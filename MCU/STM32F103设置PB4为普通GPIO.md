# STM32F103 设置 PB4 为普通 GPIO

有个项目需要使用 PB3、PB4 作为普通 GPIO，但是配置后不生效，查资料发现是 PB3、PB4 引脚在复位后的默认配置为 JTAG 功能，如果想要设置成普通 GPIO 口功能，需要在配置的时候关闭引脚的 JTAG 功能，让其可以充当普通 GPIO 口来使用。

```bash
GPIO_InitTypeDef GPIO_InitStructure;
RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA | RCC_APB2Periph_GPIOB | RCC_APB2Periph_AFIO, ENABLE);
GPIO_PinRemapConfig(GPIO_Remap_SWJ_JTAGDisable, ENABLE);
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_15;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
GPIO_Init(GPIOA, &GPIO_InitStructure); 
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_3|GPIO_Pin_4；
GPIO_Init(GPIOB, &GPIO_InitStructure);
```

上面代码中开启 AFIO 时钟，禁止使用芯片的 JTAG 功能，另外不要同时禁止芯片的 SWD 功能，否则无法烧录或仿真，经过这样的简单配置就可以充当普通 GPIO 口使用了。
