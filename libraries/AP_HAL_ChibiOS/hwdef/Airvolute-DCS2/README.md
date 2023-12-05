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
JST GH 1.25mm pitch, 3-Pin

Matching connector JST GHR-03V-S.

RC input is configured on the PPM_SBUS_PROT pin as part of the PPM connector. Pin is connected to UART3_RX and also to analog input on TIM3_CH1. This pin supports all RC protocols, but for it to be enabled, it is necessary to set SERIAL3 as RCIN.

5V supply is limited to 1A by internal current limiter.
<table border="1" class="docutils">
   <tbody>
   <tr>
   <th>Pin </th>
   <th>Signal </th>
   </tr>
    <tr>
   <td>1</td>
   <td>GND</td>
   </tr>
   <td>2</td>
   <td>5V</td>
   </tr>
   <td>3</td>
   <td>PPM</td>
   </tr>
   </tbody>
   </table>

### Bottom side
<img width="811" alt="DCS2 Pilot_top" src="https://github.com/JohnyPi/Ardupilot_md/assets/84911328/b1b8a579-005d-4d7e-a9b5-60cb3fbe06f8">

#### FMU SEC. connector
JST GH 1.25mm pitch, 12-Pin

Matching connector JST GHR-12V-S.

5V supply is limited to 1A by internal current limiter.
<table border="1" class="docutils">
   <tbody>
   <tr>
   <th>Pin </th>
   <th>Signal </th>
   </tr>
    <tr>
   <td>1</td>
   <td>GND</td>
   </tr>
   <td>2</td>
   <td>GND</td>
   </tr>
   <td>3</td>
   <td>GPIO/PWM output 4</td>
   </tr>
    </tr>
   <td>4</td>
   <td>GPIO/PWM output 3</td>
   </tr>
    </tr>
   <td>5</td>
   <td>GPIO/PWM output 2</td>
   </tr>
    </tr>
   <td>6</td>
   <td>GPIO/PWM output 1</td>
   </tr>
    </tr>
   <td>7</td>
   <td>Serial 1 RX</td>
   </tr>
    </tr>
   <td>8</td>
   <td>Serial 1 TX</td>
   </tr>
    </tr>
   <td>9</td>
   <td>Serial 2 RX</td>
   </tr>
    </tr>
   <td>10</td>
   <td>Serial 2 TX</td>
   </tr>
    </tr>
   <td>11</td>
   <td>Serial 2 RX</td>
   </tr>
    </tr>
   <td>12</td>
   <td>Serial 2 RX</td>
   </tr>
   </tbody>
   </table>

## UART Mapping

- SERIAL0 -> USB (Default baud: 115200)
- SERIAL1 -> UART1 (FMU SEC) (Default baud: 57600, Default protocol: Mavlink2 (2))
- SERIAL2 -> UART2 (FMU SEC) (Default baud: 57600, Default protocol: Mavlink2 (2))
- SERIAL3 -> UART3 (PPM) (Default protocol: None, Serial can only be set to protocol: RCIN (23))
  
UARTs do not have RTS/CTS. UARTs 1 and 2 are routed to FMU_SEC. connector.

## PWM Output

The DCS2 Onboard FMU supports up to 4 PWM outputs. All 4 PWMs are routed to FMU_SEC. connector on the board.


## Loading Firmware

Initial bootloader load is achievable only by SDW interface. Then it is possible to flash firmware thrugh onboard USB connection with Jetson host.
