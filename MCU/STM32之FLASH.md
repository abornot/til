# STM32 的 FLASH 容量问题

查看数据手册，STM32F103RCT6 是大容量产品，FLASH 为 256K，地址范围为 0x08000000 - 0x0803FFFF，有个项目写 FLASH 地址分别是 0x0804000 和 0x08060000，结果发现读写数据无任何问题。看到[有人讨论](https://www.stmcu.org.cn/module/forum/forum.php?mod=viewthread&tid=607566)，ST 的产品实际容量比标定容量大，但多出来的空间不保证质量，需要注意这个地方。
