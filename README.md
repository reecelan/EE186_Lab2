# EE186_Lab2

Part 2. 

When the button is pressed, PC13 (configured as input) goes high, which feeds a mux to ensure the right ports pin 13 is driving the EXTI line and sending and interrupt request to the NVIC. Then the typical interrupt behavior ensues:
values are pushed to the stack, the cpu pauses what is what doing as the ISR executes, and then returns to main. Because it is higher priority than main, the ISR executes in just a few clock cycles. Also, if the pending flag is never cleared, the interrupt request will never go away and it will continue to try and execute the ISR instead of continuing with main.
