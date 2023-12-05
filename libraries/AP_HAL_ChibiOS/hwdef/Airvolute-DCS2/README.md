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
 - PPM (RC input)
 - USB connection onboard with Jetson Host
 - Ethernet

## DCS2.Pilot peripherals diagram
![DC2 Pilot peripherals](https://github.com/JohnyPi/Ardupilot_md/assets/84911328/bf908b83-9ed9-4c7d-8517-7cd163f58d1b)

## DCS2.Pilot onboard FMU related connectors pinout
### Top side
<img width="818" alt="DCS2 Pilot_bottom" src="https://github.com/JohnyPi/Ardupilot_md/assets/84911328/53d0b100-b5aa-46f8-aa32-a4ba4e0890df">

#### <ins>PPM connector (RC input)</ins>
JST GH 1.25mm pitch, 3-Pin

Matching connector JST GHR-03V-S.

RC input is configured on the PPM_SBUS_PROT pin as part of the PPM connector. Pin is connected to UART3_RX and also to analog input on TIM3_CH1. This pin supports all RC protocols, but for it to be enabled, it is necessary to set SERIAL3 as RCIN. Also RC input is shared with primary FMU, so it is default disabled on secondary FMU.

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

#### <ins>FMU SEC. connector</ins>
JST GH 1.25mm pitch, 12-Pin

Matching connector JST GHR-12V-S.

The DCS2 Onboard FMU supports up to 4 PWM outputs. These are directly attached to the STM32H743 and support all PWM protocols as well as DShot and bi-directional DShot.
The 4 PWM outputs are in 2 groups:
PWM 1,2 in group1
PWM 3,4 in group2
Channels within the same group need to use the same output rate. If any channel in a group uses DShot then all channels in the group need to use DShot.

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
   <td>5V</td>
   </tr>
    </tr>
   <td>12</td>
   <td>5V</td>
   </tr>
   </tbody>
   </table>

   #### <ins>ETH EXP. connector</ins>
   505110-1692 connector
   
   Ethernet connector is routed to FMU through onboard switch.
   
   The onboard FMU is connected via the RMII bus with a speed of 100 Mbits.
   
   5V supply is limited to 1A by internal current limiter.
   <table border="1" class="docutils">
   <tbody>
   <tr>
   <th>Pin </th>
   <th>Signal </th>
   </tr>
    <tr>
   <td>1</td>
   <td>GBE_B3_P</td>
   </tr>
   <td>2</td>
   <td>GBE_B3_N</td>
   </tr>
   <td>3</td>
   <td>GND</td>
   </tr>
    </tr>
   <td>4</td>
   <td>GBE_M2_P</td>
   </tr>
    </tr>
   <td>5</td>
   <td>GBE_M2_N</td>
   </tr>
    </tr>
   <td>6</td>
   <td>GND</td>
   </tr>
    </tr>
   <td>7</td>
   <td>GBE_M1_P</td>
   </tr>
    </tr>
   <td>8</td>
   <td>GBE_M1_N</td>
   </tr>
    </tr>
   <td>9</td>
   <td>GND</td>
   </tr>
    </tr>
   <td>10</td>
   <td>GBE_M0_P</td>
   </tr>
    </tr>
   <td>11</td>
   <td>GBE_M0_N</td>
   </tr>
    </tr>
   <td>12</td>
   <td>GND</td>
   </tr>
    </tr>
   <td>13</td>
   <td>GBE_LED_LINK</td>
   </tr>
    </tr>
   <td>14</td>
   <td>GBE_LED_ACK</td>
   </tr>
    </tr>
   <td>15</td>
   <td>5V</td>
   </tr>
    </tr>
   <td>16</td>
   <td>5V</td>
   </tr>
   </tbody>
   </table>
   
## Other connectors
### CAN 1, CAN 2 connectors
The board contains two CAN buses - CAN1 and CAN 2. The buses support speeds up to 1 Mbits and in FD mode up to 8 Mbits. 

These connectors are not part of DCS2.Pilot board, but they are routed on DCS2.Adapter_board. For more informations see: https://docs.airvolute.com/dronecore-autopilot/dcs2/adapter-extension-boards/dcs2.-adapter-default-v1.0/connectors-and-pinouts

JST GH 1.25mm pitch, 4-Pin

Matching connector JST GHR-04V-S.

5V supply is limited to 1.9A by internal current limiter.
<table border="1" class="docutils">
   <tbody>
   <tr>
   <th>Pin </th>
   <th>Signal </th>
   </tr>
    <tr>
   <td>1</td>
   <td>5V</td>
   </tr>
   <td>2</td>
   <td>CAN_H</td>
   </tr>
   <td>3</td>
   <td>CAN_L</td>
   </tr>
    <td>4</td>
   <td>GND</td>
   </tr>
   </tbody>
   </table>

## UART Mapping

- SERIAL0 -> USB (Default baud: 115200)
- SERIAL1 -> UART1 (FMU SEC) (Default baud: 57600, Default protocol: Mavlink2 (2))
- SERIAL2 -> UART2 (FMU SEC) (Default baud: 57600, Default protocol: Mavlink2 (2))
- SERIAL3 -> UART3 (PPM) (Default protocol: None, Serial can only be set to protocol: RCIN (23))
  
UARTs do not have RTS/CTS. UARTs 1 and 2 are routed to FMU_SEC. connector.

## Loading Firmware

Initial bootloader load is achievable only by SDW interface. Then it is possible to flash firmware thrugh onboard USB connection with Jetson host.
