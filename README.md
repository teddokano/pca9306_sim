# PCA9306_sim
Simple analog simulation files to see [PCA9306](https://www.nxp.jp/products/interfaces/ic-spi-i3c-interface-devices/voltage-level-translators/dual-bidirectional-ic-bus-and-smbus-voltage-level-translator:PCA9306) bahavior. 

## What is this?
The [PCA9306](https://www.nxp.jp/products/interfaces/ic-spi-i3c-interface-devices/voltage-level-translators/dual-bidirectional-ic-bus-and-smbus-voltage-level-translator:PCA9306) simulation files for [LTSpice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html).  

The PCA9306 is an I²C bus voltage translator. It interfaces between signals operated with different voltage in both direction.   
The internal structure is very simple. There are 3 NMOS transistor inside, those gates are tied together. 
The internal structure is descrived in section 4 "What is a voltage translator and how it works" of [application note AN11127](https://www.nxp.com/docs/en/application-note/AN11127.pdf).  

![internal_structure](https://github.com/teddokano/pca9306_sim/blob/main/readme_img/internal_structure.png)  
_**Internal structure of NVT2002(PCA9306) from AN11127**_

This simulation is a simplified model using discrete NMOS transistor (PH2625L) model to understand how does it works.  
Characteristics of each transistor will vary. So it may not work as it is in real world but the variation is ignored in the simulation. 

# What's inside?

There are 3 types of simulation files. 

### pca9306_pass_transistor.asc
`pca9306_pass_transistor.asc` simulates a **pass transistor** static behavior.  
It will show the An pin (a SOURCE termial) follows the GATE voltage below its Vgs (gate-source voltage).  

The simulation uses a 1kΩ pull-up resistor on B-side and 1MΩ dummy load on A-side. The 1MΩ dummy load is for just fixing the An voltage. 
 
![pca9306_pass_transistor.asc](https://github.com/teddokano/pca9306_sim/blob/main/readme_img/pca9306_pass_transistor.asc.png)

### pca9306_static_behavior.asc
`pca9306_static_behavior.asc` simulates to help understanding purpose of the reference transistor.  
The simulation will show the reference transistor works as a diode to make bias voltage for the pass transistor.  
With the bias voltage from the reference transistor, the An pin is kept to Vcc(A) voltage.  

![pca9306_static_behavior.asc](https://github.com/teddokano/pca9306_sim/blob/main/readme_img/pca9306_static_behavior.asc.png)

### pca9306_operation.asc
`pca9306_operation.asc` shows how the both direction voltage translation is performed.  
Signals driven LOW from B-side (Vcc(B) = 3.3V) and A-side (Vcc(A) = 2.0V) alternatively. The HIGH voltage is kept on its Vcc on both side.  

![pca9306_operation.asc](https://github.com/teddokano/pca9306_sim/blob/main/readme_img/pca9306_operation.asc.png)


# References

- [PCA9306 atasheet](https://www.nxp.jp/products/interfaces/ic-spi-i3c-interface-devices/voltage-level-translators/dual-bidirectional-ic-bus-and-smbus-voltage-level-translator:PCA9306) 
- [Application note AN11127](https://www.nxp.com/docs/en/application-note/AN11127.pdf)
