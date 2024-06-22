# vehicleTracker

ESP32 Datasheet: https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf

Useful ESP32 tutorial website: https://randomnerdtutorials.com/esp32-i2c-communication-arduino-ide/

Write unit and which pins you plan to use for the subsystem:
- Default pins for I2C are GPIO21(SDA = PIN 33) and GPIO22(SCL = PIN 36)
- SDA = PIN 33
- SCL = PIN 36

H3LIS100DL (accelerometer) pin connection

NC = Not connected it can be left floating

The left hand side numbers are the H3LIS100DL pins and the right hand side are the ESP32 pin numbers

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

SFH 5701 A01 (Light sensor)

Left number is light sensor pin and right number is other pins
1. -> ADC input
2. -> Pin 2 (Vdd)
Connect Rload between GND and ADC input
Notes:
- Pin 1 is anode(output) and Pin 2 is cathode (Vdd)
- We could include LPF.

Pin out pic:
![image](https://github.com/joshuarythomas/vehicleTracker/assets/68773192/1149a803-13f7-4a12-92c1-72cc0ad02fb9)


TLA2024IRUGT (ADC) pin out
Left is ADC pin numnber
Right is either ESP32 or peripheral - if it just says pin X then it refers to pin X of the ESP32 otherwise it specifies peripheral
1. -> Pin 1 (GND)
2. NC - leave floating!
3. -> Pin 1 (GND)
4. -> SFH 5701 A01 Pin 1 
5. -> External breakout
6. -> External breakout
7. -> External breakout
8. -> Pin 2 (Vdd) with decoupling Cap
9. -> Pin 33 (SDA)
10. -> Pin 36 (SCL)

Float unused analog inputs, or tie unused analog inputs to GND.

Pin out pic:
![image](https://github.com/joshuarythomas/vehicleTracker/assets/68773192/6d40b782-5c36-4a83-b890-f431cd2af26b)


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

COST:
- https://docs.google.com/spreadsheets/d/1ha0QW2Twl-Rdmpq9GGSAH3WqHdwXN5mQoQr_CWo1MlU/edit?gid=0#gid=0

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Accelerometer:
- H3LIS100DL
- Datasheet: https://au.mouser.com/datasheet/2/389/h3lis100dl-1849125.pdf
- Mouser link: https://au.mouser.com/ProductDetail/STMicroelectronics/H3LIS100DLTR?qs=v3MacVxtdDLHj8sdza6BGw%3D%3D
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
- Crash Detecion calculator: https://www.omnicalculator.com/physics/car-crash-force
- This estimates that you can experience around 50g when driving at 50kph for a person weighing 75kg with a seat belt!
- This website sugests that around 30 g's is typical in crash: https://jrlawfirm.com/blog/auto-accidents/car-accident-g-force/#:~:text=According%20to%20GSU's%20HyperPhysics%20Project,collision%20with%20a%20fixed%20object.
- Good to have accelerometer that can measure up to at least 30g I reckon for our purposes.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Light Sensor
- SFH 5701 A01
- Datasheet: https://au.mouser.com/datasheet/2/588/prd_pim_datasheet_5690474_EN_pdf-3419424.pdf
- Appendix sheet: https://look.ams-osram.com/m/6d9facb9506ab4a2/original/Ambient-light-sensor-SFH-5701.pdf
- Mouser link: https://au.mouser.com/ProductDetail/ams-OSRAM/SFH-5701-A01?qs=sGAEpiMZZMsMHNolIrhXrHsmG3VqP4YXp4aw0dWdt7mNf16qlKnKtw%3D%3D
- Has PCB symbol and footprint
- In stock
- Cheap
- Analog
- Helpful setup schematic on appendix doc
- Photodiode
- Will need a load resistor
Helpful note: https://electronics.stackexchange.com/questions/192264/how-to-compute-bias-resistor-for-phototransistor-value

Calculations: Light Sensor:
- Assuming we'll just power using 3V3.
- 90% of FS (3.3V) = 2.97V
- Assumign we get no more than 10000lx correspons to max Iout = 10mA
- 1.45V minimum headroom (VDD – VOUT) so if necessary reduce Rload.
- So Vdd - Vout > 1.45V so Vout < 1.85V.
- So Rload = 1.85V / 10mA = 185 ohms
- The using f3db = 1/(2(pi)ReqC) where Req is the equivalent Req = Rload + R
- Choose C = 330pf why not and F3db = 50Hz
- So R = 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

ADC
- TLA2024IRUGT
- Datasheet: https://www.ti.com/lit/ds/symlink/tla2024.pdf?ts=1718851900522&ref_url=https%253A%252F%252Fau.mouser.com%252F
- Mouser link: https://au.mouser.com/ProductDetail/Texas-Instruments/TLA2024IRUGT?qs=chTDxNqvsylxt6cbA39OGw%3D%3D
- Cheap
- In stock
- 12 bit res good enough
- 4 channel sweet
- PCB footprint + symbol check
- I2C
- 2V to 5.5V Vdd
- delta sigma is fast
- up to 3.3 kSPS should be fast enough


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

GPS Module
- LCL86L 
- Datasheet: [quectel_lc86l_hardware_design_v1-0.pdf](https://github.com/user-attachments/files/15923197/quectel_lc86l_hardware_design_v1-0.pdf)
- Mouser link: https://www.mouser.com/ProductDetail/Quectel/LC86LICMD?qs=iLbezkQI%252BsiFPFQjIwBL1Q%3D%3D
- Has footprint
- Documentation seems fine
- $20 the cheapest one that seems decent.
- UART
- Size is small
- Horizontal positioning accuracy: 2.5m
- Update rate: 1 Hz (max. 10 Hz) good enough for slow moving vehicles
- 3.3V 30mA current draw pretty standard for gps power consumption
- 37 channels hoefully it will be fine around buildings.
- TTFF: 35 seconds
- sensitivity is around -140dBm good enough.
- Supports Galileo

GPS Selection guide:
- 
- https://www.sparkfun.com/GPS_Guide

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Micro switch
- SAJ25YXRHL147SDTSEQ
- Datasheet: https://au.mouser.com/datasheet/2/418/8/ENG_DS_2351450_A-2887325.pdf
- Mouser link: https://au.mouser.com/ProductDetail/TE-Connectivity-Alcoswitch/SAJ25YXRHL147SDTSEQ?qs=7MVldsJ5Uaw0Eh4bvIT51g%3D%3D
- $1.70

Mechanical Design
- Mount the micro switch on the PCB or the internal surface of the casing such that the lever is depressed when the casing is closed.
- Ensure the lever is released when the casing is opened.
Lever Actuation:
- Position the switch so that the lever aligns with a part of the casing cover. When the cover is closed, it should press down on the lever, keeping the switch in the "closed" position.
- When the cover is opened, the lever should be released, putting the switch in the "open" position.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Choosing capacitors
- this link says go for thin film over ceramic: https://electronics.stackexchange.com/questions/69919/ceramic-vs-film-capacitor-which-one-is-preferred-in-audio-circuits
- This link suggests ceramic should be fine: https://resources.altium.com/p/which-type-capacitor-should-you-use

