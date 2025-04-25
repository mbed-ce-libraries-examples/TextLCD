# TextLCD library for MbedCE

Library for interfacing many variants of Character Liquid Crystal Displays under MbedCE.

## How to start
1. Create a new project according to [MbedCE instructions](https://github.com/mbed-ce/mbed-os/wiki)
2. Add this as submodule to your project via `git submodule add --depth 1 https://github.com/mbed-ce-libraries-examples/TextLCD TextLCD`
3. The top level `CMakeList.txt` (in root of your project) should be modified according to [this wiki page](https://github.com/mbed-ce/mbed-os/wiki/MbedOS-configuration#libraries-in-your-application)
4. Create your main.cpp file and copy & Paste example code below.
5. Visit [TextLCD/TextLCD_confg.h](https://github.com/mbed-ce-libraries-examples/TextLCD/blob/main/TextLCD_Config.h) and change configuration according to your hardware. Some hints below.
6. Build the project

## Example code
```
// example for LCD 16x2 with i2c expander (aliexpress)
#include "mbed.h"
#include "TextLCD.h"

// fill your I2C pins in to I2C api object
I2C i2cBus(I2C_SDA,I2C_SCL); 

// I2C bus, PCF8574 GPIO expander Slaveaddress, LCD Type
TextLCD_I2C lcd(&i2cBus, PCF8574A_SA7, TextLCD::LCD16x2);

DigitalOut led(LED1);

int main()
{
    printf("MbedCE_lib_example_TextLCD\r\n");

    lcd.cls();
    lcd.setCursor(TextLCD::CurOff_BlkOff);
    lcd.setBacklight(TextLCD::LightOn);
    thread_sleep_for(200);
    lcd.printf("Welcome to\nMbedCE community\n"); 
    while(1) {
        led = !led;
        thread_sleep_for(1000);                     
    }
}
```
## Description
TextLCD is very advanced library what supports
* many sizes from 6x1 to 40x4.
* Parallel port (4bits = just 4 data bits), I2C-Bus or SPI communication.
* few GPIIO Expanders over I2C/SPI
* also several design options. For Example DFROBOT and ADAFRUIT make their own designs of PCBs, and then the expander mapping are different and so on.

All these settings are necessary to configure in TextLCD_confg.h file before you start. With wrong settings you will no see correct behavior of your display.

## Troubleshooting
it is very easy to make a mistake so here are some tips
* when you see the first line of your LCD is full of squares then your display does not communicate with your MCU. Check conection and settings of TextLCD_confg.h
* when your LCD makes non logic behavior like nonsense jumping of cursor the backlight is off instead of on. Check settings of [TextLCD_confg.h](https://github.com/mbed-ce-libraries-examples/TextLCD/blob/0138191528adcedd54738c94cecc8ba49447f74d/TextLCD_Config.h#L71-L80), probably wrong expander is selected
  
Feel free to ask [MbedCE-LE - discussions](https://github.com/orgs/mbed-ce-libraries-examples/discussions)

### Status:
This library was tested (02/2024) with Nucleo-F446RE, 16x2LCD with i2C expander (PCF8574), VS-Code under Win11, GCC 12.3 and MbedCE library
