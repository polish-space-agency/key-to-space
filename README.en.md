<p align="right">
  <a href="README.md">Polski</a> | <b>English</b>
</p>

<p align="center">
  <img src="images/polsa-logo.png" alt="Polish Space Agency" width="220">
</p>

# Key to Space

```
PROJECT LICENSE NOTICE

EN: All contents of this repository, including KiCad design files (schematics and PCB layouts) and technical documentation, are licensed under:
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0).

The full license legal code is available at: https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.txt

SPECIFIC TERMS AND AUTHOR'S INTENT:
1. NON-COMMERCIAL USE: Copying, modifying, and manufacturing physical units of this device is permitted strictly for non-commercial, private, hobbyist (e.g., amateur radio operators, makers), and non-profit/NGO institutional purposes.
2. SPECIAL PERMISSION FOR EDUCATIONAL INSTITUTIONS: Official schools, universities, and educational organizations are explicitly authorized to manufacture and order the production of this hardware (including batch PCB fabrication from commercial manufacturers) solely for their own internal educational and instructional purposes.
3. PCB ATTRIBUTION (THE "BY" CONDITION): In accordance with the Attribution requirement, it is strictly forbidden to remove, alter, or obscure the author's identification (name, handle, or logo) placed on the silkscreen layer of the PCB. Any manufactured circuit board must retain these markings in their original form.

```

**Technical documentation – educational electronic device, school version**

The project was commissioned by the Polish Space Agency (POLSA) for educational activities related to the IGNIS mission. The IGNIS mission was carried out by the Ministry of Development and Technology, the Polish Space Agency and the European Space Agency.
The device was manufactured in 100,000 units and distributed free of charge to Polish schools.

In response to requests sent to POLSA, the project has been made available to hobbyists and anyone interested in using it for non-commercial purposes.

<p align="center">
  <img src="images/okladka.jpg" alt="Key to Space – assembled device" width="600">
</p>

## Table of contents

- [Abbreviations](#abbreviations)
- [1. Introduction](#1-introduction)
- [2. Technical specification](#2-technical-specification)
- [3. Device description](#3-device-description)
- [4. Bill of materials (BOM)](#4-bill-of-materials-bom)
- [5. Tests](#5-tests)
- [6. Manufacturing information](#6-manufacturing-information)

## Abbreviations

| Abbreviation | Meaning |
|-------|-------------|
| BOM   | Bill of Materials |
| FR    | Flame Retardant |
| HAL   | Hot Air Leveling |
| ISS   | International Space Station |
| LED   | Light-Emitting Diode |
| PCB   | Printed Circuit Board |
| STEM  | Science, Technology, Engineering, Mathematics |
| THT   | Through-Hole Technology |
| USB   | Universal Serial Bus |

## 1. Introduction

This technical documentation contains key information about the educational electronic device *Key to Space*, designed for the Polish Space Agency. The device (a PCB with a set of components for self-assembly) is part of a larger educational programme promoting STEM and will be used to teach the basics of electronics and soldering in schools.

The documentation contains the technical specification, a description of the device's design and operation, and information useful for possible manufacturing of the device.

## 2. Technical specification

### 2.1. Dimensions

Satellite-shaped PCB. Typical laminate thickness – 1.57 mm (0.063 in). The board has six mounting holes with a diameter of 3.2 mm.

![Figure 1: PCB dimensions](images/01-wymiary-pcb.png)

*Figure 1: PCB dimensions*

### 2.2. Assembly

The device is intended for self-assembly, which is why it uses easy-to-solder through-hole (THT) components.

![Figure 2: Board with soldered components](images/02-plytka-z-elementami.png)

*Figure 2: Board with soldered components*

Total weight of the device (PCB with components): approx. 40 g.

### 2.3. Power supply

The circuit can be powered with a DC voltage from 3 V to 9 V. This allows a wide choice of power sources – e.g. USB (power adapter, charger, laptop, power bank) or common batteries (1.5 V AA or AAA).

Maximum current consumption: below 200 mA.

## 3. Device description

The device consists of two independent analog electronic circuits that perform the following functions:

- **telegraph key** – a circuit that emits a sound when the button is pressed,
- **clap detector** – a circuit that responds to sound by lighting up LEDs.

The design uses a varied set of electronic components, such as resistors, capacitors, transistors, integrated circuits, LEDs, sound transducers and mechanical parts. This varied set of components is a valuable educational tool for users, who can learn about the applications of different components and understand how they work and how they interact.

### 3.1. Design

#### 3.1.1. PCB

The PCB is double-sided (two-layer), covered with a blue solder mask with markings on the component side. The side wings, resembling a satellite's solar panels, are not part of the electronic circuit – they serve only as decoration and a place for logos.

![Figure 3: PCB – component side](images/03-pcb-strona-elementow.png)

*Figure 3: PCB – component side*

![Figure 4: PCB – solder side](images/04-pcb-strona-lutowania.png)

*Figure 4: PCB – solder side*

#### 3.1.2. Component placement

The figure below shows a visualisation of the printed circuit board with the placed components, divided into the electronic circuits that perform specific functions.

![Figure 5: Component placement on the PCB](images/05-rozmieszczenie-komponentow.png)

*Figure 5: Component placement on the PCB (labels: ZŁĄCZE ZASILANIA – power connector, KLASKACZ – clap detector, KLUCZ TELEGRAFICZNY – telegraph key)*

### 3.2. Telegraph key

The electronic circuit implementing the telegraph key consists of the following elements:

- tactile switch,
- astable oscillator,
- piezoelectric buzzer.

Pressing the momentary tactile switch (S1) powers the astable oscillator circuit, which generates an alternating signal for the piezoelectric buzzer (BZ1). The buzzer converts the alternating voltage into an acoustic signal.

![Figure 6: Telegraph key circuit diagram](images/06-schemat-klucz-telegraficzny.png)

*Figure 6: Telegraph key circuit diagram*

The astable oscillator built around the NE555P timer (U1) is a simple yet versatile solution for generating square waves with variable frequency and duty cycle. Its flexibility, reliability and ease of implementation make it a popular choice in many electronic applications.

During operation, capacitor C4 is cyclically charged and discharged. The NE555P controls this process and switches the logic state of output Q, producing a periodic square wave.

Capacitor C3 suppresses fast changes of the reference voltages supplied to U1 from the internal divider.

The frequency of the generated waveform can be calculated using the formula:

$$f = \frac{1.44}{(R_4 + 2R_5)\,C_4}$$

Duty cycle of the generated waveform:

$$D = \frac{R_4 + R_5}{R_4 + 2R_5}$$

The resistances R4 and R5 and the capacitance of C4 directly affect the frequency and duty cycle of the generated waveform:

- increasing C4 lengthens the cycle time and therefore lowers the frequency,
- increasing R4 lengthens the high state (*Time High*) but does not affect the low state (*Time Low*),
- increasing R5 lengthens both the high state (*Time High*) and the low state (*Time Low*) and reduces the duty cycle (down to a minimum of 50%).

The signal fed to the buzzer can be observed by connecting an oscilloscope to test points TP1 and TP2 (ground) on the PCB.

The figure below shows the calculations for the component values used in the circuit.

![Figure 7: Calculated waveform parameters for R4=10kΩ, R5=2.2kΩ and C4=100nF](images/07-obliczenia-r4-10k.png)

*Figure 7: Calculated waveform parameters for R4 = 10 kΩ, R5 = 2.2 kΩ and C4 = 100 nF*

The parameters of the actual waveform may differ from the calculated ones due to the tolerances of the components used.

![Figure 8: Actual waveform observed on an oscilloscope](images/08-oscyloskop-r4-10k.png)

*Figure 8: Actual waveform observed on an oscilloscope*

Changing R4 to 15 kΩ lowers the frequency of the generated waveform.

![Figure 9: Parameters after increasing R4](images/09-obliczenia-r4-15k.png)

*Figure 9: Parameters after increasing R4*

![Figure 10: Waveform after increasing R4](images/10-oscyloskop-r4-15k.png)

*Figure 10: Waveform after increasing R4*

Swapping R4 and R5 and reducing C4 to 22 nF increases the frequency of the generated waveform and lowers the duty cycle. This may improve the sound of the buzzer.

![Figure 11: Increasing the frequency of the generated waveform](images/11-obliczenia-wyzsza-czestotliwosc.png)

*Figure 11: Increasing the frequency of the generated waveform*

![Figure 12: Actual waveform after increasing the frequency](images/12-oscyloskop-wyzsza-czestotliwosc.png)

*Figure 12: Actual waveform after increasing the frequency*

Instead of the piezoelectric buzzer, an electromagnetic buzzer (also without a built-in oscillator) can be used. The PCB has holes matching the smaller lead pitch and diameter of this type of component.

### 3.3. Clap detector

The clap detector circuit consists of:

- a microphone with a preamplifier,
- a signal amplifier,
- an LED indicator.

The microphone responds to changes in ambient sound pressure, producing a varying output voltage proportional to the sound intensity. This signal is amplified and used to drive the LEDs.

![Figure 13: Clap detector circuit diagram](images/13-schemat-klaskacz.png)

*Figure 13: Clap detector circuit diagram*

The electret microphone used (MK1) features small size, low output impedance and a wide frequency range. This type of microphone has a built-in preamplifier in the form of a field-effect transistor. The transistor must be powered from an external voltage source through the bias resistor R1, which also acts as the load. The value of this resistor is chosen to provide the correct operating voltage for the microphone, and it also affects the gain. Capacitor C2 at the output removes the DC component.

Transistors Q1 and Q2 amplify the microphone signal and drive the LEDs. Changes in the microphone signal cause changes in the collector current of Q2, thereby changing the LED brightness. Resistor R3 can be used to adjust the LED brightness.

## 4. Bill of materials (BOM)

### 4.1. Components mounted on the PCB

All components are through-hole (THT).

| Item | Value/type | Description | Package | Part number – example |
|---------|-------------|------|---------|-------------------------------|
| R1 | 4.7kΩ[^1] | Carbon film resistor, 0.25W, ±5% | Axial, Ø2.3x6mm | CF1/4W-4K7 |
| R2 | 1MΩ | Carbon film resistor, 0.25W, ±5% | Axial, Ø2.3x6mm | CF1/4W-1M |
| R3 | 10kΩ[^2] | Carbon film resistor, 0.25W, ±5% | Axial, Ø2.3x6mm | CF1/4W-10K |
| R4 | 10kΩ[^3] | Carbon film resistor, 0.25W, ±5% | Axial, Ø2.3x6mm | CF1/4W-10K |
| R5 | 2.2kΩ | Carbon film resistor, 0.25W, ±5% | Axial, Ø2.3x6mm | CF1/4W-2K2 |
| C3 | 10nF | Ceramic capacitor, 50V | 2.54mm | CC-10N |
| C4 | 100nF[^4] | Ceramic capacitor, 50V | 2.54mm | CC-100N |
| C1 | 100µF | Electrolytic capacitor, 25V | Ø6x11mm, 2.5mm | EWH1EV101E11OT |
| C2 | 1µF | Electrolytic capacitor, 50V | Ø5x11mm, 2.5mm | EWH1HM010D11X25T |
| C5 | 10µF | Electrolytic capacitor, 50V | Ø5x11mm, 2.5mm | EWH1HM100D11X25T |
| U1 | NE555P | Integrated circuit, timer | DIP8 | NE555P |
| Q1, Q2 | BC547B[^5] | NPN bipolar transistor | TO92 | BC547B |
| D1..D5 | | LED, diffused, blue, up to 1000mcd | 5mm, domed | L-7113QBDL-D |
| MK1[^6] | | Electret microphone, 1..10V, 0.5mA, -44dB (min.) | Ø9.7mm, 2.5mm | LD-MC-9765P |
| BZ1 | | Piezoelectric buzzer without oscillator, 1..10V, 1mA | Ø13.8x6.8mm, 7.6mm | AT-1438-TWT-R |
| S1 | | Momentary tactile switch | 12x12x4.3mm | TACT-24N |
| J1 | | Screw terminal, 90° angled, 2-pin | 5.08mm | 282837-2 (TE CONNECTIVITY) or TB-5.08-P-2P/BL |

Additional components included in the kit (for experiments, not permanently mounted):

| Item | Alternative for | Quantity |
|---------|:-------------:|:------------:|
| Resistor 4.7kΩ | R3 | 1 |
| Resistor 15kΩ | R3, R4, R5 | 2 |
| Resistor 30kΩ | R3 | 1 |
| Ceramic capacitor 22nF | C4 | 1 |

[^1]: Alternatively 10kΩ, depending on the sensitivity of the microphone used – increasing the resistance may improve the operation of the clap detector.
[^2]: Changing R3 depending on the supply voltage changes the LED brightness – at higher supply voltages, increasing the resistance reduces the LED brightness and in some cases may improve the sound of the buzzer (suggested additional resistors: 4.7kΩ, 15kΩ and 30kΩ).
[^3]: Other values of R4 and R5 should be added to the kit to allow experiments with the parameters of the generated waveform (suggested additional resistor: 15kΩ).
[^4]: Like R4 and R5, the capacitance of C4 also directly affects the parameters of the generated waveform, so another capacitance value should also be added to the kit (e.g. 22nF).
[^5]: The circuit has also been tested with other NPN transistors (BC183, BC546, BC548, BC549, BC550).
[^6]: The best results were achieved with an OEM microphone whose part number, manufacturer and datasheet could not be determined – the table lists the alternative component used in the ISS version. The OEM microphone is available under the code UCC-00740.

### 4.2. Additional components

Suggested additional components depending on the chosen power source:

- battery holder for 2 or 3 batteries (AA or AAA) with leads – 1 pc. included in the kit (2× AAA holder),
- solderable USB type A plug – 1 pc.

The battery holder or the prepared cable with a USB plug should be connected to the screw terminal on the PCB (marked J1), observing the correct polarity.

| ![Figure 14: 2xAAA battery holder](images/14-koszyk-baterie.png) | ![Figure 15: USB plug with housing](images/15-wtyczka-usb.png) |
|:---:|:---:|
| *Figure 14: 2xAAA battery holder* | *Figure 15: USB plug with housing* |

Optional mounting hardware:

- polyamide standoffs (M3, 10mm) – 6 pcs,
- nylon screws (M3, 6mm) – 6 pcs.

## 5. Tests

### 5.1. Current consumption

The device has low power consumption. Tests using a power analysis module (*Power Profiler Kit*) as the power source showed that during normal operation at a 5 V supply voltage, peak current does not exceed 150 mA.

![Figure 16: Current consumption during operation at 5V supply](images/16-pobor-pradu-5v.png)

*Figure 16: Current consumption during operation at 5 V supply*

![Figure 17: Current consumption while using the telegraph key](images/17-pobor-pradu-klucz.png)

*Figure 17: Current consumption while using the telegraph key*

![Figure 18: Inrush current at device power-up](images/18-prad-rozruchowy.png)

*Figure 18: Inrush current at device power-up*

## 6. Manufacturing information

### 6.1. PCB – technical specification

| Parameter | Value |
|----------|---------|
| Laminate type | FR-4 |
| Board outline dimensions | 153x82mm (1.26dm²) |
| Base laminate thickness | 1.55mm |
| Number of layers | 2 |
| Copper thickness | 35µm (1oz) |
| Number of holes | 58 + 6 mounting holes |
| Plated through-holes | Yes |
| Solder mask | Both sides, blue |
| Surface finish | HAL |
| Non-standard board shape | Yes |
| Board and hole milling | Yes |
| Silkscreen | One side, white |
