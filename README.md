# PPS5330_PowerSupply_mod
Reverse Engineered Firmware for the ELV PPS5330 Power Supply and hardware modification for faster output voltage slew rate

![20240418_200517](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/1e9c6e01-77a0-45ae-b5b4-699f695727ae)

![Umbau](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/06558d7d-171d-4dcb-a2f9-a04866291bf2)


* All Basic functionality is working, the Power Supply is in a usable state
* Added Temperature measuring of the internal heatsink and transformer with display on LCD
* PWM controlled FAN dependend on Heatsink's Temperature
* Voltage Calibration
* Current Calibration
* faster output voltage slew rate
* Measure transformer temperature
* Menu with LCD contrast/backlit settings
* Calibration of internal ADC measurements
* Timeout for Display-Settings-Menu

Temperature display: Long time is heatsink, short time is transformer.

Video: https://youtu.be/KPteA9frJQY

# Hardware modification
In the ELV PPS5330 power supply, the setpoint specification for voltage and current is implemented by the Atmega MCU with PWM signals. The PWM signals I-Soll and I-Soll are converted into a proportional DC voltage via a low-pass filter R43/C27 and R53/C34. The problem in the power supply is the low PWM frequency of 488Hz and the low pass filter. A rapid increase in current and voltage after a standby is therefore not possible. When activating the output, the power supply needs 1.4 seconds until the voltage is fully present at the output.

Output voltage rise rate
![Bild_1](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/4eb7f483-c800-4026-afd7-3867d3b0ba49)

Output voltage rise rate after modification
![Bild_2](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/7543e44e-1874-4d4a-b0e7-1bc3348c964e)

Modification circuit. The PWM signal for I-Soll and U-Soll at R43/R53 is now constantly present in the new firmware and is no longer switched off by standby. A CMOS switch IC1 switches off the rectified PWM voltage on the regulator input IC4/B pin 5 and IC4/C pin 10. The CMOS switch IC 1 receives its control signal from the inverted standby signal. The advantage of this circuit is that there is no time required for filtering of the PWM signal. After the hardware modification, the voltage rise rate is < 50msec (Pic).

Modification circuit
![Screenshot 2024-04-19 225535](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/c07e47ff-2ca1-4e27-b3c3-4703c8ddaa33)

![Screenshot 2024-04-19 230514](https://github.com/rolfdegen/PPS5330_PowerSupply_mod/assets/16689445/52f20a49-0b4a-4445-8b75-58de71420227)











  
