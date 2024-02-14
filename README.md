# TextLCD library for MbedCE

Library for interfacing many variants of Character Liquid Crystal Displays under MbedCE.

## How to start
1. Create a new project according to [MbedCE instructions](https://github.com/mbed-ce/mbed-os/wiki)
2. Add this as submodule to zour project via `git submodule add --depth 1 https://github.com/mbed-ce-libraries-examples/TextLCD TextLCD`
3. The top level `CMakeList.txt` (in root of your project) should be modified according to [this wiki page](https://github.com/mbed-ce/mbed-os/wiki/MbedOS-configuration#libraries-in-your-application)
4. Create your main.cpp file and copy & Paste example code below.
5. Visit [TextLCD/TextLCD_confg.h](https://github.com/mbed-ce-libraries-examples/TextLCD/blob/117de5e049de8f8351fbb2466a282d648d5f918a/TextLCD_Config.h#L70) and change configuration according to your hardware. Some hints below.
6. Build the project

## Example code
```
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
* many sizes form 6x1 to 40x4.
* Parallel port (4bits = just 4 data bits), I2C-Bus or SPI communication.
* few GPIIO Expanders over I2C/SPI
//TODO

### Status:
This library was tested (02/2024) with Nucleo-F446RE, 16x2LCD with i2C expander (PCF8574), VS-Code under Win11, GCC 12.3 and MbedCE library
