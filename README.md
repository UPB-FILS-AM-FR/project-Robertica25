# Deck Check

| Author | Popa Robert Alexandru |
|--------|-----------------|


## Description
This project is a smart device that automatically determines how many playing cards remain in a standard card deck, using a precision load cell and a high-resolution 24-bit ADC module.
 
The idea stems from a simple problem: when playing board games or card games, it is often tedious to manually count how many cards are left in the deck — especially after multiple rounds of dealing. This system solves that problem in an elegant, non-invasive way, without modifying the card pack and without requiring a camera or complex image processing.
 
The system uses a 1kg load cell connected to an HX711 24-bit ADC amplifier module to measure the weight of the card pack with high precision. Since each standard playing card weighs approximately 1.78g and the empty box weight is known and set as tare at startup, the ATmega328P microcontroller on the Arduino Uno calculates the number of remaining cards by dividing the net weight by the weight of a single card. The result is displayed in real time on a TM1637 4-digit 7-segment display.

## Motivation
The goal of this project is to demonstrate practical usage of a high-precision external ADC (24-bit) paired with an ATmega328P, while building something useful for everyday recreational activities.
 
This project is relevant because:
 
- It demonstrates the use of an HX711 external ADC with two-wire serial communication, distinct from standard SPI or I2C.
- It combines multiple concepts: GPIO and ADC calibration.
- It provides a robust, lighting-independent solution — unlike camera-based approaches.
- It can be adapted for any product with a known per-unit weight (medicine pills, coins, poker chips, etc.).

## Architecture
The system is structured around the following hardware modules:
 
The **Arduino Uno (ATmega328P)** is the central processing unit. It continuously reads data from the HX711 module, computes the card count, and updates the display.
 
The **1kg load cell** is the mechanical sensor that deforms proportionally to the weight placed on it. It generates a differential millivolt-range voltage signal that is fed into the HX711 module via the E+/E-/A+/A- connections.
 
The **HX711 module** is a 24-bit ADC and amplifier dedicated to load cells. It communicates with the Arduino Uno via a two-wire protocol on pins DAT=D7 and CLK=D8.
 
The **TM1637 4-digit 7-segment display** shows the current number of cards remaining in the pack. It communicates with the Arduino Uno via its own two-wire protocol on pins CLK=D2 and DIO=D3.
 
**Power** is supplied via the Arduino Uno USB cable. The HX711 module and the TM1637 display are powered from the same 5V rail.
### Block diagram


### Components
| Device | Usage | Price |
|--------|-------|-----------|
| Arduino Uno (ATmega328P) | Central processing unit | 29 RON |
| TM1637 4-digit display | Displays the remaining card count | 9 RON |
| HX711 GroundStudio module | 24-bit ADC for the load cell | 7 RON |
| Load cell 1kg | Measures the weight of the card pack | 11 RON |
| Breadboard + jumper wires | Circuit prototyping and assembly | 48 RON |

### Libraries

| Library | Description | Usage |
|---------|-------------|-------|
| `HX711_ADC` | Driver for the HX711 24-bit ADC module | Used to initialize the two-wire communication and read the weight value from the load cell. |
| `TM1637Display` | Driver for TM1637 4-digit 7-segment displays | Used to initialize the CLK/DIO interface and display the computed card count. |



