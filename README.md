# STM32F407ZETx_TIM_DMA_ADC
STM32F407ZETx_TIM_DMA_ADC

- 定时器触发ADC DMA转换（1s触发一次）

- 输入信号40KHz

- ADC 采样率 1.4MHz（84MHz / (12+采样时间) * (2 * 分频系数)）（84MHz / (12+3) * (2 * 2)）=  1.4 MHz

- 总转换时间计算：
  - TCONV = 采样时间 + 12个周期
  - 例如：
    - 当ADCCLK = 42MHz 和 3 Cycles 周期的采样时间，TCONV  = 3 + 12 = 15 周期 = 0.36 us

- 如果我们的输入信号是 20KHz （周期为 50us），若要将它恢复出来，一个周期最少采样20个点，此时采样率要达到400KHz，所以ADC的采样率必须在400KHz 以上。为了达到最好的精度，我们选取ADC时钟为12MHz，即6分频。在12MHz 以及保证采样率的情况下，采样时间越长其，准确性就越好。

- STM32CubeMX ADC 配置：

  - Parameter Settings:
    - Scan Conversion Mode    ---> Enable
    - Continuous Conversion Mode   ---> Enable
    - DMA Continuous Requests   ---> Enable

  - DMA Setting:
    - DMA Mode	--->	Circular
    - Data Width    --->    Word
