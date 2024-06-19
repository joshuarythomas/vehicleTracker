# vehicleTracker

ESP32 Datasheet: https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf

Useful ESP32 tutorial website: https://randomnerdtutorials.com/esp32-i2c-communication-arduino-ide/

Write unit and which pins you plan to use for the subsystem:
- Default pins for I2C are GPIO21(SDA) and GPIO22(SCL)


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


