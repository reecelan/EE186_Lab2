# EE186_Lab2

Part 2. 

When the button is pressed, PC13 (configured as input) goes high, which feeds a mux to ensure the right ports pin 13 is driving the EXTI line and sending and interrupt request to the NVIC. Then the typical interrupt behavior ensues: values are pushed to the stack, the cpu pauses what is what doing as the ISR executes, and then returns to main. Because it is higher priority than main, the ISR executes in just a few clock cycles. Also, if the pending flag is never cleared, the interrupt request will never go away and it will continue to try and execute the ISR instead of continuing with main.

Part 3.

The prescaler (PSC) slows down the hardware clock whose ticks are counted by CNT. When CNT reaches the auto reload register (ARR) it resets to zero and an event update triggers. It raises a flag that triggers that ISR. Meanwhile the clock continues to run so the next event update happens on schedule. This periodicity is different from an external interrupt which is triggered by manual events like a button push.

f_clk_cnt = f_clk_psc/1+psc -> set PSC = 3,999 so f_clk_cnt is 1kHz. (Something like 1MHz would be too large to store in ARR). Then set ARR=999 so f_interupt = f_clk_cnt/(ARR+1) = 1Hz (which is the same as period of 1s).
