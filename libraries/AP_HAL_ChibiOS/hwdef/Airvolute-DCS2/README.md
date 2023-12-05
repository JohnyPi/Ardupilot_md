# Onboard FMU on Airvolute DCS2.Pilot board

https://docs.airvolute.com/dronecore-autopilot/dcs2


## Features

 - MCU: STM32H743
 - IMU: BMI088 
 - Barometer: BMP390
 - 2 UARTS
 - 2 CAN buses
 - 4 PWM outputs 
 - Buzzer output
 - USB connection onboard with Jetson Host

## UART Mapping

 - SERIAL0 -> USB
 - SERIAL1 -> UART2 (Telem1)
 - SERIAL2 -> UART3 (Telem2)

UARTs do not have RTS/CTS. Both UARTs are routed to FMU_SEC. connector.

## RC Input
 
RC input is configured on the UART3_RX and is connected also to analog input on TIM3_CH1. Rc input is routed to onboard connector (JST 3-pin )
  

## PWM Output

The DCS2 Onboard FMU supports up to 4 PWM outputs. All 4 PWMs are routed to FMU_SEC. connector on the board.


## Loading Firmware

Initial bootloader load is achievable only by SDW interface. Then it is possible to flash firmware thrugh onboard USB connection with Jetson host.
