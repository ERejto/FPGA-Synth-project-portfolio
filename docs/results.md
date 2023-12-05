# Results

## New Hardware

## Design Decisions

### C Program Architecture

Interrupts and RTOS were not used on the micro-controller C program to enable reading signals and sending things to the FPGA. 

### Note and Wave Type Widths

Notes and wavetypes were chosen to have a bit width of 4. This was done so the note to be played and both carrier and modulation wave could be sent in the same SPI send. The consideration with the note width was that it had to provide for values greater than 12 for the 12 notes in 1 key. Then wave types were left at 4 bits to match. This provides a lot more room to program different wavetypes. the only restriction on this is LUT space on the fpga. 

### ADC Resolution and FPGA settings 

A bit resolution of 6 bits was chosen for the ADC to match a bit width of fpga settings. This was done to keep adding and multiplying with small widths. This was also done to be able to transfer 2 settings per SPI send. This could be upgraded to 14 bits and 1 setting per SPi send. This would mainly provide more resolution in configuring frequency modulation as currently the 6 bit settings are shifted left to provide the necessary range. It would also provide for more filter configurations however it would require developement of a more sophisticated filter module. 

## Video Links

## Audio Files

