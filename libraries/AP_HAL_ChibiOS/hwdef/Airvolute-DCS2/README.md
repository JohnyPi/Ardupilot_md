# Onboard FMU on Airvolute DCS2.Pilot board
For more informations on DCS2.Pilot board see:
https://docs.airvolute.com/dronecore-autopilot/dcs2


## Features

 - MCU: STM32H743
 - IMU: BMI088 
 - Barometer: BMP390
 - 2 UARTS
 - 2 CAN buses
 - 4 PWM outputs
 - RC input
 - Buzzer output
 - USB connection onboard with Jetson Host
 - Ethernet

## DCS2.Pilot peripherals diagram
![DC2 Pilot peripherals](https://github.com/JohnyPi/Ardupilot_md/assets/84911328/bf908b83-9ed9-4c7d-8517-7cd163f58d1b)

## DCS2.Pilot onboard FMU related connectors pinout
### Top side
<img width="818" alt="DCS2 Pilot_bottom" src="https://github.com/JohnyPi/Ardupilot_md/assets/84911328/53d0b100-b5aa-46f8-aa32-a4ba4e0890df">

#### PPM connector (RC input)
RC input is configured on the PPM_SBUS_PROT pin as part of the PPM connector. Pin is connected to UART3_RX and also to analog input on TIM3_CH1. This pin supports all RC protocols, but for it to be enabled, it is necessary to set SERIAL3 as RCIN.


### Bottom side
<img width="811" alt="DCS2 Pilot_top" src="https://github.com/JohnyPi/Ardupilot_md/assets/84911328/b1b8a579-005d-4d7e-a9b5-60cb3fbe06f8">

## UART Mapping

 - SERIAL0 -> USB
 - SERIAL1 -> UART2 (Telem1)
 - SERIAL2 -> UART3 (Telem2)

UARTs do not have RTS/CTS. Both UARTs are routed to FMU_SEC. connector.

## RC Input
 
RC input is configured on the UART3_RX and is connected also to analog input on TIM3_CH1. Rc input is routed to onboard PPM connector.
  

## PWM Output

The DCS2 Onboard FMU supports up to 4 PWM outputs. All 4 PWMs are routed to FMU_SEC. connector on the board.


## Loading Firmware

Initial bootloader load is achievable only by SDW interface. Then it is possible to flash firmware thrugh onboard USB connection with Jetson host.
