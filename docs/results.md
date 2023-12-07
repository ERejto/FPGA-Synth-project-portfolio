# Results

## New Hardware
There are three pieces of "new" hardware used in this design. The first is the the SPI DAC. While initially we wanted to utilize the MCU's onboard DAC to do data conversions, we ran into speed problems and moved onto a higher resolution better quality DAC. The second piece of new hardware is the MCU's ADC peripheral. This peripheral works by scanning through a multiple ADC channels at a high speed and writing these values to memory. The channels used on the ADC are configurable and in our case we configured the ADC to scan through four channels at maximum speed. The last piece of "new" hardware is the FPGA's MAC block. This MAC was necessary to implement FM since this operation requires fast multiplication and addition. 

## Design Decisions

### C Program Architecture

Due to the speed requirements of our system, interrupts were not required. The code polls the GPIO pins and ADC pins for changes, then sends these changes via SPI. Each poll takes about 100 clock cycles which at a 16 MHz ends up being a 160 kHz sampling rate. 

### Note and Wave Type Widths

Notes and wavetypes were chosen to have a bit width of 4. This was done so the note to be played and both carrier and modulation wave could be sent in the same SPI send. The consideration with the note width was that it had to provide for values greater than 12 for the 12 notes in 1 key. Then wave types were left at 4 bits to match. This provides a lot more room to program different wavetypes. the only restriction on this is LUT space on the fpga. 

### ADC Resolution and FPGA settings 

A bit resolution of 6 bits was chosen for the ADC to match a bit width of fpga settings. This was done to keep adding and multiplying with small widths. This was also done to be able to transfer 2 settings per SPI send. This could be upgraded to 14 bits and 1 setting per SPi send. This would mainly provide more resolution in configuring frequency modulation as currently the 6 bit settings are shifted left to provide the necessary range. It would also provide for more filter configurations however it would require developement of a more sophisticated filter module. 

## Video Links

## Audio Files

