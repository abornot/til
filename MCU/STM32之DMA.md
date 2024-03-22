# STM32F4 的 DMA 需要清除标志位才可以再次传输，而 STM32F1 却不需要

最近有个项目使用 STM32F407 USART1 串口发送数据，借助 DMA 方式，发现一个问题：需要检测发送完成标志位后清除标志位后才能再次发送，而之前使用 STM32F103 却不需要清标志位的操作，清除标志位的代码如下：

```bash
if (DMA_GetFlagStatus(DMA2_Stream7, DMA_FLAG_TCIF7) != RESET)
{ 
  DMA_ClearFlag(DMA2_Stream7, DMA_FLAG_TCIF7);
}
```
