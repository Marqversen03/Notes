---
tags:
link:
Date: 12-12-2025
---

The dashboard display will use a PCB designed to hold the LCD screen from the UM3223 Discovery Kit. The goal of this PCB is to replace the bottom plate of the Discovery Kit with a more specialized and efficient solution tailored to our needs. Additionally, the PCB should allow control of four LEDs that will be located on the dashboard.

a block diagram is drawn

![[PCB - Block_diagram.canvas]]

## Indicator Rules
Rules for Each LED Located on the Dashboard

**AMS**

- **EV 5.8.9**  
    A red indicator light in the cockpit that is easily visible from inside and outside the cockpit even in bright sunlight and clearly marked with the lettering **AMS** must light up if and only if the AMS opens the SDC. It must stay illuminated until the error state has been manually reset, see EV6.1.6. Signals controlling this indicator are SCS, see T11.9.

**TS OFF**

- **EV 4.10.10**  
    A green indicator light in the cockpit that is easily visible even in bright sunlight and clearly marked with **TS off** must light up if TSAL green light is on, see EV4.10.3.

**IMD**

- **EV 6.3.8**  
    A red indicator light in the cockpit that is easily visible from inside and outside the cockpit even in bright sunlight and clearly marked with the lettering **IMD** must light up if and only if the IMD opens the SDC. It must stay illuminated until the error state has been manually reset, see EV6.1.6. Signals controlling this indicator are SCS, see T11.9.

**LV**

- No specific rule mentioned, but it should indicate low-voltage system status.



### General LED Rules

- **T 11.10**  
    Any system status light(s), see T6.3 and T14.9, must meet the following requirements:
- Black background
- Rectangular, triangular, or near-round shape
- Minimum illuminated surface of **15 cm²** with even luminous intensity
- Clearly visible in very bright sunlight
- If LED lights are used without a diffuser, they must not be more than **20 mm apart**
- If a single line of LED lights is used, the minimum length is **150 mm**

**Meaning**
The led must be clearly labbeled with a black background. The following colors is to be used 

| System | indicator       | 
| ------ | --------------- |
| TS OFF | Green indicator |
| IMD    | Red indicator   |
| AMS    | Red indicator   |
| LV     | Green indicator |


## PCB Design

The PCB will be designed around the STM32U5G9ZJ microcontroller, which is the same as the one used in the UM3223 kit. We want the PCB to communicate with the LCD screen, which requires a 2×25-pin connector, and with the LEDs, which require one ground and one power supply pin for each LED. The LV LED will be on when the STM32 has power. Additionally, to communicate with the system, we will use a CAN bus.

**Outputs:**

- 2×25 pins (LCD screen)
- 3 + 1 pins (3 LED pins + GND) // no LV
- 2 pins (CAN bus)

The LEDs must be clearly visible in sunlight, which means they will require higher current and possibly a transistor for switching.
## PCB Power supply
The STM32 is designed to operate at 3.3 V, and the LCD screen also runs on 3.3 V. However, the LCD backlight requires 5 V.  
To provide this, we can use a buck converter to step down the car’s power supply and generate both 3.3 V and 5 V outputs.

We also want the system to run from both the car and a computer, so we can test and program it in the workshop while ensuring it works in the car. By placing a header and a jumper, we can easily select the power source.

### STM32 Power supply
The STM32 microcontroller has several different power supply domains, each serving a specific purpose:

| Name         | Power       | Purpose                      | Need it? |
| ------------ | ----------- | ---------------------------- | -------- |
| VDD          | 1.71-3.6    | General power                | YES      |
| VSS          | 0v          | Ground                       | YES      |
| VDDA         | 1.6-3.6     | ADC/DAC/OPAMP/COMP           | YES      |
| VSSA         | 0v          | Analog Ground                | YES      |
| VBAT         | 1.65-3.6    | RTC + Backup SRAM/registre   | YES      |
| VDDIO2       | 1.08-3.6    | Seperate I/O Supply PG(15.2) | NO       |
| VDDUSB       | 3.0-3.6     | USB Transceiver              | M        |
| VDD11        | 1.1V        | Core logic / SRAM            | YES      |
| VDDSMPS      | 1.71-3.6V   | Intern Step down             | YES      | 
| VLXSMPS      | Switch-node | Inductor                     | YES      |
| VDDDSI       | DSI         | MIPI DSI interface           | NO       |
| VDD11USB     | 1.0-1.26V   | USB Core                     | NO       |
| VREF+ /VREf- | REF  ADC    | ADC/DAC REF                  | YES      |
All power supplies require specific capacitors to maintain a stable flow. While basic rules can help determine these values, in our case, the capacitor values have already been defined and implemented in the UM3223 kit, so we will copy those values:

**VDD**

- 10 × 100 nF (one capacitor per VDD pin)
- 1 × additional 10 µF

**VDDA**

- 1 × 100 nF
- 1 × 1 µF

**VBAT**

- 1 × 100 nF capacitor

**VDD11**

- 1 × 2.2 µH inductor
- 2 × 2.2 µF capacitors
- 
> [!note]
The table does not specify whether wires need to be connected to the pins. Even if certain pins are not in use, they may still need to be connected to 3.3 V or GND.

### Power Regulation
To regulate the core logic power, we need a regulator. In this microcontroller, there are two options: LDO and SMPS.

**LDO (Low Dropout Regulator)**  
This is a linear regulator. It regulates power by dissipating the surplus voltage as heat, which makes it less efficient. However, it is easier to implement on the PCB.

**SMPS (Switch-Mode Power Supply)**  
This is a switching regulator. It regulates power by rapidly switching and using an inductor (2.2 µH) to step down the voltage. It is more efficient and generates less heat, though the circuit is more complex.

We have chosen to implement an SMPS because, despite its complexity, it is better suited for powering an RGB LCD screen. And we can always internally switch to LDO.

#### EMI
When dealing with coils, there is a likelihood of electromagnetic interference (EMI). To mitigate this, we need to implement the following safety measures:

- Minimize the loop area
- Use a solid ground layer
- Place capacitors close to the supply and ground
- Shield the coil
- Keep SMPS away from the LCD, clock lines, and analog circuits
- Filter VDDA using a ferrite bead and capacitor

Because the LDO is an internal regulator, we always have the option to switch if interference becomes too high.

---

**ADC/DAC**  
To read low-level analog signals from AMS, TS, and IMD, we need to connect Vref+ to the analog ground. This is because the reference buffer is between VDDA and Vref+.



## Display CN3
The display is fairly straightforward, with 50 pins arranged in a 2×25 grid. All connections are solid with no components, except for the following:

**SDA (Pin 38) / SCL (Pin 40)**

- 2 × 0 Ω resistors or jumper resistors

**BL_5V (Pin 45) / BLGND (Pins 47, 49)**

- 2 × 0 Ω resistors
- 1 × 100 nF capacitor
- 1 × 10 µF capacitor

**VDD (Pin 50)**

- 1 × 100 nF capacitor

![[CN3_Layout.png]]

## Crystal:
To operate our LCD screen, we want a high clock speed, but increasing it too much makes the system more expensive. To achieve a clean yet not excessive performance, we have chosen a 16 MHz crystal (830069392).  
According to the datasheet, we use two 10 pF capacitors. For extra precision, a 0 Ω resistor can be placed at both ends for stabilization. This is not strictly necessary, but if we buy in bulk, there’s no reason not to include it.

>We sure?
In the UM3223 kit, they also use a 32.768 kHz crystal for sleep mode and low-power operation. We see no reason to include this feature.


## Flash memory
For memory, the UM3223 uses OctaFlash, which helps with fast booting and is capable of storing large files such as fonts and images. We have three options:

**1. Use the STM32**  
It has 4 MB of internal Flash and 3 MB of SRAM. With a screen resolution of 800×480, we can handle 24-bit color, which requires about 1.15 MB—no problem. However, we are limited when it comes to storing images, fonts, and other assets in internal flash.

**2. Use OctaFlash**  
Purchasing one online is possible and would give us extreme flexibility, but it comes at a cost. Additionally, OctaFlash is soldered underneath the component, which means we would need specialized tools.

**3. Use an SD card**  
This is also possible, but it won’t work the same way. We would need a method to store and access the data, and boot times and frame rates would not be as good. However, it would allow us to store large files.

>For now
For now, I will develop using internal memory and…

## LED GPIO
To control the four LEDs, we need to find three pins that can provide a signal. These should output an analog signal, so most pins will work. We can use **PB1**, **PB7**, and **PB8**, as these are currently not in use.

Additional LEDs that could be useful:

- **Boot**
- **Power**
- **Extra**

### LED PCB
We want the LEDs to sit on a separate PCB so they can be positioned away from the center. A basic PCB has been drawn to visualize the components and overall size.

| **3D Render**                     |     | **Basic Schematic (with transistor)** |
| --------------------------------- | --- | ------------------------------------- |
| ![[Indicator_rough(3d).jpg\|256]] |     | ![[Indicator_rough(SCH).jpg\|256]]    |

We plan to use DIP LEDs so they can protrude from a 3D-printed enclosure and be clearly visible to the driver without exposing the PCB. This also creates the opportunity for a waterproof area where the PCB can reside.

## CAN bus
To communicate, we can use a CAN bus. Here, we choose a classic CAN type. The STM32 already has implemented **TXL** and **RXL** pins that we can use.  
To utilize these, we need a **CAN transceiver**.   here we use a ATA6563. 
The datasheet provides a curcuit we can copy to our schematic

![[ATA6563.png]]


the pins are locates 
TX = PH13 (87)
RX = PH14 (90)


## Schematic

### VDD
To supply the power demand of 3v3 we use a regulator that can output a consistent 3v3 volt. the power comes from the VBUS terminal. wich is the power from the cars battery.
![[3v3.png]]

Another regulator is used for the backlight of the LCD-Screen. we get this by a regulator direktly from the cars battery.


we choose to regulate both power inputs through the vbus to elimminate noise from regulating from vbus to 5v to 3v3.
![[5v.png]]


### STM32
![[STM32.png]]


### VDD

as mention earlier the mcu need power in specifik pins for our specifik perpours, and each needs some capacitors to keep a steady flow.
![[VDD.png]]


### Crystal
To control the clk we use a 16 MHz crystal, and install it, as the data sheet shows with the capacitors/values.

![[CLK.png]]

### CN3
To connect to the LCD Screen we copy the CN3 port from the UM 3223

![[CN3.png]]


### USB
![[USB.png]]



### CAN
![[CAN.png]]



## TODO

- [ ] USB
- [ ] 3v3
- [ ] 5v
- [ ] CN3
- [ ] CAN Transiver
- [ ] connect
- [ ] NRST
- [ ] Crystal
- [ ] Boot
- [ ] Ferrit bead
- [ ] ST_LINK
- [ ] LED_cntrl




> [!warning]
> Check at CN3 ikke er spejlvendt

> [!question]
>- Signals AMS, TS & IMD
>	- Where from
>	- How much
>- NRST



## Parts

### Active Components

##### Crystal (CLK)

##### Regulator


### Passive Components

##### Capacitor

| Component | amount | Part number |
| --------- | ------ | ----------- |
| 100n      |        |             |
| 2.2u      |        |             |
| 1u        |        |             |
| 10u       |        |             |
| 10p       |        |             | 
| 22u       |        |             |
| 4.7u      |        |             |
| 10n       |        |             |

##### Resistor
| Component | amount | Part number | 
| --------- | ------ | ----------- |
| 1k        |        |             |      
| 0         |        |             |      
| 10k       |        |             |      

##### Coil
| Component | amount | Part number | 
| --------- | ------ | ----------- |
| 2.2uH     | 1      |             |       

##### Ferrit bead
| Component | amount | Part number | 
| --------- | ------ | ----------- |
| 120R     | 1      |             |       

##### Button
| Component | amount | Part number |
| --------- | ------ | ----------- |
| XXX       | 2      |             |

##### LED
| Component | amount | Part number |
| --------- | ------ | ----------- |
| Red       | 1      |             |     
| Green     | 1      |             |     



## BOM List




## Links

ATA6563
https://www.mouser.dk/datasheet/3/282/1/ATA6562.3-Data-Sheet-20005790E.pdf

UM3223
[Discovery kit with STM32U5G9ZJ MCU - User manual](https://www.st.com/resource/en/user_manual/um3223-discovery-kit-with-stm32u5g9zj-mcu-stmicroelectronics.pdf)

STM32
[WE Part Data Sheet V1.0025](https://www.we-online.com/components/products/datasheet/830069392.pdf)