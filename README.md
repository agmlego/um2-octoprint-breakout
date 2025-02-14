This is a breakout for octoprint, compatible with the Ender3S1 display.


### Pinout
| J1 Pin | GPIO Pin | Mux      | Purpose                 |
|--------|----------|----------|-------------------------|
| 3      | 2        |          | N/C                     |
| 5      | 3        | `GPIO3`  | Power button            |
| 7      | 4        | `TXD3`   | Display, `UART3`        |
| 8      | 14       | `TXD0`   | Printer, `UART0`        |
| 10     | 15       | `RXD0`   | Printer, `UART0`        |
| 11     | 17       | `GPIO17` | Power button blue LED   |
| 12     | 18       | `PWM0`   | Pi cooling fan PWM      |
| 13     | 27       | `GPIO27` | Power button red LED    |
| 15     | 22       | `GPIO22` | Printer power-on detect |
| 16     | 23       | `GPIO23` | Printer power relay     |
| 18     | 24       | `GPIO24` | Power button green LED  |
| 19     | 10       | `SDA5`   | I2C header, `I2C5`      |
| 21     | 9        |          | N/C                     |
| 22     | 25       |          | N/C                     |
| 23     | 11       | `SCL5`   | I2C header, `I2C5`      |
| 24     | 8        |          | N/C                     |
| 26     | 7        |          | N/C                     |
| 27     | 0        | `ID_SD`  | HAT+ EEPROM, `I2C0`     |
| 28     | 1        | `ID_SC`  | HAT+ EEPROM, `I2C0`     |
| 29     | 5        | `RXD3`   | Display, `UART3`        |
| 31     | 6        |          | N/C                     |
| 32     | 12       | `GPIO12` | Encoder click           |
| 33     | 13       | `GPIO13` | Display beeper          |
| 35     | 19       | `GPIO19` | Encoder channel B       |
| 36     | 16       |          | N/C                     |
| 37     | 26       | `GPIO26` | Encoder channel A       |
| 38     | 20       |          | N/C                     |
| 40     | 21       |          | N/C                     |

### Images
[Interactive BOM](bom/ibom.html)

### Device Tree Overlay
```
# Power button
dtoverlay=gpio-shutdown
# Automated blower control
dtoverlay=pwm-gpio-fan,fan_gpio=18
# Printer power
gpio=23=op,dl
# LEDs
dtoverlay=gpio-led,gpio=17,label=blue,trigger=actpwr
dtoverlay=gpio-led,gpio=24,label=green
dtoverlay=gpio-led,gpio=27,label=red
# Display controls
dtoverlay=gpio-key,gpio=12,label=knobpress,keycode=256
dtoverlay=rotary-encoder,pin_a=19,pin_b=26,relative_axis=1
# Display UART
dtoverlay=uart3
# Beeper
gpio=13=op,dl
# Power sense
gpio=22=ip,np
# I2C
dtoverlay=i2c5,pins_10_11=1,baudrate=400000
```