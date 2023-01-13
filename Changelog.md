Change log for Transistor Switch
=======================================

Version 1.0 (06/05/22) - Rochelle De Silva
----------------------
- Simulated a Transistor Switch circuit to turn on and off one LED. There were three different resistances simulated for R1 and R2. R1 and R2 were kept the same value for simulation. Initially R1 and R2 were set at 10,000 Ohm; however, this was way too big a resistance because the simulated output displayed that the current through the LED was 150-160 microAmps, which is not on the order of magnitude of 10-15 mA which is the current required to turn the LED on. LED's require a supply voltage of at least 2V and a forward current of around ~14-20 mA for a red LED(depends on the color and size of the LED). Thus, the resistance of R1 and R2 was increased to 1000 Ohm; however, this was also too large a resistance, giving an output current in the range of 1.4-1.6 mA. The resistance was finally increased to 100 Ohm for both R1 and R2. This displayed results of the current going through the LED as around 14-16 mA, which is exactly what is necessary for the LED to turn on properly.
- A DC sweep was initially conducted, however this was changed in LTSpice to be a transient simulation because the outcome is looking at the response with respect to time. The input voltage V2 was changed to be a pulse between +/-2V and period of 2 seconds and a time switched on of 0.5 seconds (thus a time switched off of 1.5 seconds).

Added to LTSpice Simulation directory:
- LTSpice_Circuit.png
- LTSpice_Simulation_100_Ohm.png
- LTSpice_Simulation_1000_Ohm.png
- LTSpice_Simulation_10000_Ohm.png

Known Problems:
- Currently this Transistor Switch circuit is for one LED. In order to have four separate, independent LEDs which turn off and on with the various directions of the eye movement (i.e., left, right, up down), this transistor switch circuit simulated in LTSpice must be replicated another three more times. 


Version 2.0 (07/05/22) - Rochelle De Silva
----------------------
- A Transistor Switch circuit is built utilizing a blue LED. There is a supply voltage from the Analog Discovery of 5V (red lead). There is voltage of 2V given to the circuit from the Waveform Generator 1 lead (yellow). Two different resistance values were used for R1 and R2 (keeping R1 = R2 throughout). The first resistors used are 100 Ohm resistors (as simulated in LTSpice). The circuit with the LED switched on and off with 100 Ohm resistors can be found in the images **TransistorSwitch_Circuit_100_Ohm_Blue_On.jpeg** & **TransistorSwitch_Circuit_100_Ohm_Blue_Off.jpeg** respectively. The resistors were then swapped for 1000 Ohm resistors in the circuit. The circuit with the LED switched on with the 1000 Ohm resistors can be found in the image **TransistorSwitch_Circuit_1000_Ohm_Blue_On.jpeg**.

Added to Circuit directory:
- TransistorSwitch_Circuit_1000_Ohm_Blue_On.jpeg
- TransistorSwitch_Circuit_100_Ohm_Blue_Off.jpeg
- TransistorSwitch_Circuit_100_Ohm_Blue_On.jpeg

Known Problems:
- Circuit must be adapted so that there are four LEDs which turn off and on with various directions of the eye movement.
- Circuit must also be altered so that the input is the EOG signal rather than a test sine wave/square wave.


Version 3.0 (07/05/22) - Rochelle De Silva
----------------------
- For the Transistor Switch circuit with the Blue LED, both sine and square waves are used as test signals. A 1 kHz Frequency and a period of 2 seconds is utilized for the test signals. Originally, a period of 1ms was utilized in the test wave, but the LED was flashing too fast, so the period was increased to 2 seconds to see the flash of the LED more distinctly. Two different resistance values were also utilized (keeping R1 = R2) of 1000 Ohm and 100 Ohm. When using the 100 Ohm resistors in the circuit, the blue LED light was brighter than the when 1000 Ohm resistors were utilized in the circuit. When the 1000 Ohm resistors were utilized, the blue LED light was slightly dimmer. This is due to the fact that a current across the LED of 10-16 mA is required for the LED to operate (as found in the LTSpice simulations), and this occurs when there are 100 Ohm resistors in the circuit. When there are 1000 Ohm resistors, only 1.4 - 1.6 mA of current is going through the LED.
- The 1000 Ohm resistors square wave and sine wave inputs on WaveForms can be found in the images **TransistorSwitch_SquareWave_1000_Ohm.png** & **TransistorSwitch_SineWave_1000_Ohm.png** respectively.
- The 100 Ohm resistors square wave and sine wave inputs on WaveForms can be found in the images **TransistorSwitch_SquareWave_100_Ohm.png** & **TransistorSwitch_SineWave_100_Ohm.png** respectively.

Added to Waveforms Input directory:
- TransistorSwitch_SquareWave_1000_Ohm.png
- TransistorSwitch_SquareWave_100_Ohm.png
- TransistorSwitch_SineWave_1000_Ohm.png
- TransistorSwitch_SineWave_1000_Ohm.png

Known Problems:
- A period and frequency need to be decided upon for the final Transistor Switch for the LED. Right now it is just set to a period of 2 seconds and a frequency of 1 kHz. However, this could change depending on the EOG signal coming in. Thus, this will be determined in later steps of the project.
