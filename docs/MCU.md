---
layout: page
title: MCU
---

# MCU Design

The purpose of the MCU is to read in the values the buttons and potentiometers and send the configurations to the FPGA. To do this GPIO, ADC, and SPI was used.

- [MCU Design](#mcu-design)
  - [Main](#main)
  - [GPIO](#gpio)
  - [ADC](#adc)
  - [SPI](#spi)


## Main

The Main program combines the below functionality in the correct way to update settings and play notes on the FPGA. This is done by running a loop that samples ADC values and button presses. Then if the read in values change from the previous interation of the loop, it sends the corresponding setting to the FPGA. This is not the most robust system and could be improved by using interupts.

## GPIO

GPIO was used to read when buttons are pressed. It does this by reading values from each GPIO pin and one hot encoding the pressed button every sample. This value is then encoded using a recursive 16 -> 4 bit encoder. 

## ADC

ADC is implemented to read the values from the pots. It does this by waiting for the conversion flag then reading the ADC value during a conversion sequence. In each conversion sequence the correct value is stored an array. This array is passed back to the main.

## SPI

SPI is used to send information to the FPGA. SPI is a one way link and the MCU is the controller and the FPGA is the peripheral. This is done with 16 bit sends from MCU to FPGA. See the FPGA page for an example send.