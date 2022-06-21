# Metal-Detector
Implemented a detector alarms  when a metal is within a 10-cm range for a coin-picker robot or devices in need of detecting metals.

Demo link: https://youtu.be/ArRpMJVE5u0

Author: Ruyi Zhou
Student #: 49581911
Date: Apr.8th 2020
Project: Metal Detector
Funtion: The speaker will sound on and the alert red light will be turned on if a metal is closing to the detector.

Constrcution:

The microsystem is Pic32 which is connected to computer by BO230XS board. The output of the BO230XS board is 5V
and the output pin connects to a MCP1700 regulator to generate a 3.3V. The CBUS3 pin is connected with 'reset' 
button. TXD, RXD, RTS, CTS are connected to the Pic32 system. The VDD voltage of Pic32 is 3.3V. In addition, 
pin14 is connected to a metal detector which is consist of a NOT gate and a capacitor, a inductor and a resistor. The
NOT gate is consist of a N-type MOSFET and a P-type MOSFET. Pin15 on Pic32 is connected to a speaker.


Software:

The main code is the provided 'Period.c'. This code will generate the frequency of Pin 14 (the detector).First,
I use:
	#define SYSCLK 40000000L
	#define Baud2BRG(desired_baud)( (SYSCLK / (16*desired_baud))-1)
	#define FREQ 4800L // 2Hz or 0.5 seconds interrupt rate
and
	__ISR(_TIMER_1_VECTOR, IPL5SOFT) Timer1_Handler
from 'TimerIRQ.c' to setup an interupt. Then, I create a function according to 'blinky.c' to call the 'SetupTimer1'
function. Finally, in my main function, there is while(1) loop which will detect the frequency constantly. If a
metal is close the frequency will decrease. I set a threshold value which is the frequncy with a closer metal.
If the detective frequency is lower than the threshold, the speaker will sound up, and the putty will print "A metal
is closer!!!!" and the detective frequency. Otherwise, if the detector cannot detect a signal, the putty will
print 'NO SIGNAL".


Operation of Detector:

The inductor is connected to a CMOS (NOT GATE), so it will generate a periodical function on the oscillator which 
means there is a frequency. When a metal is closer to the inductor, the magnetic field is changing and so the 
inductence will be slightly changed. It is reflected as a change in the oscillator frequency.


Extra feature:

I combined the alert light with speaker. If a metal is closing the alert light will bright to indicate the close
of metal.


Reference:
[1] Z. Zhang, Y. Liu and Knovel, Academic, Electronics & Semiconductors, High Frequency MOSFET Gate Drivers: 
Technologies and Applications. 2017.

