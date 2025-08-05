# August 4th: Planned my PCB and found components

So today, across two sessions, I decided the components of my PCB. My PCB is meant to be a teaching tool where beginners can learn about various sensors and hardware in general. I don't know if I'm the most qualified person to make this because I barely have experience, but nonetheless it was fun. With the help of a lot of Google, I got it...sorta. I don't actually know if it will work. I chose the ATmega328P-AU as my microcontroller. It is powered by either Micro USB(also used for programming) or 3 AAA batteries. The concept of the whole PCB is like a demonstration of all these different components. You use a rotary encoder to choose which component you want(accelerometer, photoresistor, thermistor). It then outputs on either the RGB LED or the OLED screen.

Here is my plan for the project:
1. Decide components ✅
1. Upload components to Kicad - going to take longer than y'all think
1. Design schematic
1. Design PCB - wiring and organization
1. Code firmware
1. Create website for tutorial

My vision for the project is once you have the PCB, you can mess around with the sensors to learn how they work. You can then look on the website to add features and learn about the components with written text.

## BOM(My only output from today - also replacement for images because I have none):

### 🔌 POWER SUPPLY
| **Component**                         | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                                    |
| ------------------------------------- | ----------------- | ------- | -------------- | --------- | -------------------------------------------- |
| **RT9080-33GJ5 (3.3V LDO Regulator)** | C841192           | 1       | \$0.1034       | \$0.10    | Powers 3.3V components like IMU and OLED     |
| **AMS1117-5.0 (5V LDO Regulator)**    | C6187             | 1       | \$0.1913       | \$0.19    | Regulates to 5V from battery                 |
| **3xAAA Battery Holder**              | C5370880          | 1       | \$1.6500       | \$1.65    | Main power input source                      |
| **1N5819WS Schottky Diode**           | C191023           | 1       | \$0.0096       | \$0.01    | Reverse polarity protection on battery input |
| **Slide Switch SS‑3390S‑L2**          | C318997           | 1       | \$0.1239       | \$0.12    |SMD slide switch to turn battery power on/off |

### 🧠 MICROCONTROLLER AND PROGRAMMING
| **Component**              | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                   |
| -------------------------- | ----------------- | ------- | -------------- | --------- | --------------------------- |
| **ESP32-WROOM-32D-N4**     | C473012           | 1       | \$2.7315       | \$2.73    | Main microcontroller        |
| **Micro-USB Connector**    | C7507410          | 1       | \$0.0494       | \$0.05    | USB interface connector     |
| **Tactile Button (Reset)** | C2888545          | 1       | \$0.0053       | \$0.01    | Manual reset for MCU        |

### 📟 OUTPUT COMPONENTS
| **Component**                | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                     |
| ---------------------------- | ----------------- | ------- | -------------- | --------- | ----------------------------- |
| **RGB LED (WS2812B 3535)**   | C110402           | 1       | \$0.0840       | \$0.08    | For colorful visual feedback  |
| **0.96" OLED Display (I2C)** | C5248080          | 1       | \$1.9710       | \$1.97    | Main display interface (3.3V) |
| **Passive Piezo Buzzer**     | C22387762         | 1       | \$0.0479       | \$0.05    | For sound feedback            |

### 🧭 INPUT COMPONENTS
| **Component**                | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                               |
| ---------------------------- | ----------------- | ------- | -------------- | --------- | --------------------------------------- |
| **Rotary Encoder w/ Button** | C398936           | 1       | \$2.8740       | \$2.87    | Multi-function input (direction + push) |
| **Tactile Button**           | C2888545          | 1       | \$0.0053       | \$0.01    | General-purpose user input              |


### 🌡️ SENSORS
| **Component**                          | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                 |
| -------------------------------------- | ----------------- | ------- | -------------- | --------- | ------------------------- |
| **ICM-42688-P (Accelerometer + Gyro)** | C1850418          | 1       | \$2.4675       | \$2.47    | 3.3V I2C IMU sensor       |
| **GL5528 Photoresistor (LDR)**         | C10081            | 1       | \$0.0377       | \$0.04    | Analog light sensor       |
| **10kΩ NTC Thermistor**                | C77130            | 1       | \$0.0103       | \$0.01    | Analog temperature sensor |

### 📶 I2C & LOGIC LEVEL CONVERSION
| **Component**             | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                                   |
| ------------------------- | ----------------- | ------- | -------------- | --------- | ------------------------------------------- |
| **BSS138 MOSFET**         | C52895            | 2       | \$0.0476       | \$0.10    | Used for I2C level shifting (bidirectional) |
| **4.7kΩ Resistor (0805)** | C17673            | 4       | \$0.0017       | \$0.04    | I2C pull-ups (x2), gate pull-downs (x2)     |

### ⚙️ PASSIVES
| **Component**              | **JLCPCB Part #** | **Qty** | **Unit Price** | **Total** | **Notes**                                               |
| -------------------------- | ----------------- | ------- | -------------- | --------- | ------------------------------------------------------- |
| **10kΩ Resistor (0402)**   | C25744            | 3       | \$0.0005       | \$0.03    | Pull-ups: Reset (1), Thermistor divider (1), Button (1) |
| **330Ω Resistor (0805)**   | C17630            | 3       | \$0.0018       | \$0.03    | Series resistors for RGB LED                            |
| **1µF Capacitor (0805)**   | C15850            | 3       | \$0.0108       | \$0.03    | Decoupling caps for regulators and logic                |
| **100nF Capacitor (0805)** | C49678            | 4       | \$0.0044       | \$0.04    | MCU decoupling (AVCC, VCC) and CH340 bypass             |
| **Green LED (0603)**       | C165983           | 1       | \$0.0221       | \$0.02    | Power indicator                                         |                                     |

**Total time spent: 5h** - I know that is a lot, but I am a beginner with like no knowledge.
