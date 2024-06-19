# vehicleTracker

ESP32 Datasheet: https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf

Useful ESP32 tutorial website: https://randomnerdtutorials.com/esp32-i2c-communication-arduino-ide/

Write unit and which pins you plan to use for the subsystem:
- Default pins for I2C are GPIO21(SDA = PIN 33) and GPIO22(SCL = PIN 36)
- SDA = PIN 33
- SCL = PIN 36

H3LIS100DL (accelerometer) pin connection
NC = Not connected it can be left floating
Tghe left hand side numbers are the H3LIS100DL pins and the right hand side are the ESP32 pin numbers
If the SA0 pad is connected to ground, the LSB value is ‘0’ (address is then 0011000b)

1. -> Pin 2 (Vdd)
2. NC
3. NC
4. -> Pin 36 (SCL)
5. -> Pin 1 (GND)
6. -> Pin 33 (SDA)
7. -> Pin 1 for GND (SA0 least sig bit of device address)
8. -> Pin 2 (Vdd high for I2C)
9. -> Pin 31 (GPIO19 for interrupt 2)
10. -> Pin 1 (GND)
11. -> Pin 33 (GPIO21 for interrupt 1)
12. -> Pin 1 (GND)
13. -> Pin 1 (GND)
14. -> Pin 2 (Vdd)
15. -> Pin 2 (Vdd)
16. -> Pin 1 (GND)

Pin out pic
<img width="792" alt="Screenshot 2024-06-19 at 11 48 03 PM" src="https://github.com/joshuarythomas/vehicleTracker/assets/68773192/d6efaf53-195d-4c3f-9733-72af7ba70f9d">
Power supply decoupling capacitors (100 nF ceramic, 10 μF aluminum) should be placed as near as possible to pin 14 of the device (common design practice).

COST:
- https://docs.google.com/spreadsheets/d/1ha0QW2Twl-Rdmpq9GGSAH3WqHdwXN5mQoQr_CWo1MlU/edit?gid=0#gid=0

Accelerometer:
Crash Detecion calculator: https://www.omnicalculator.com/physics/car-crash-force
- This estimates that you can experience around 50g when driving at 50kph for a person weighing 75kg with a seat belt!
- This website sugests that around 30 g's is typical in crash: https://jrlawfirm.com/blog/auto-accidents/car-accident-g-force/#:~:text=According%20to%20GSU's%20HyperPhysics%20Project,collision%20with%20a%20fixed%20object.
- Would be good to have accelerometer that can measure up to 30g I reckon for our purposes.

H3LIS100DL
- In stock
- up to +- 100g
- 3-axis very good
- low power
- operates from 2.16V to 3.6V
- I2C/SPI
- data output up to 400Hz probs good enough
- only 8 bit resolution not great but its the cheapest
- $8 by far the cheapest
- Has PCB symbol and footprint
- Datasheet: https://au.mouser.com/datasheet/2/389/h3lis100dl-1849125.pdf
- Mouser link: https://au.mouser.com/ProductDetail/STMicroelectronics/H3LIS100DLTR?qs=v3MacVxtdDLHj8sdza6BGw%3D%3D


