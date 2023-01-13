Change log for Instrumentation Amplifier
=======================================

Version 1.0 (09/05/22) - Rochelle De Silva
----------------------
- A Instrumentation Amplifier circuit is built utilizing a INA126PA amplifier. There is a positive supply voltage (red lead) of 5V and a negative supply voltage of -5 V (white lead) from the Analog Discovery. 

- A resistance value of 1.782 kOhms (R_G) is utilized to connect to the gain setting pin. This resistance was found by looking on the INA126PA datasheet. It is recommended that for a gain of 50 a resistance value of 1.78 kOhms is utilized across the gain setting pins. Although the R_G value used is 0.002 kOhms off from the recommended R_G value in the datasheet for INA126PA, the expected output should not change drastically and this error will be taken into account for further analysis. 

- The Instrumentation Amplifier circuit with the 1.782 kOhm resistance can be found in the images **InstrumentationAmplifier_InProgressCircuit_1882_Ohm_Resistor.jpeg**.

Added to Circuit directory:
- InstrumentationAmplifier_InProgressCircuit_1882_Ohm_Resistor.jpeg

Known Problems:
- The resistance value utilized for R_G (1.782 kOhms) is 0.002 kOhms off from the recommended R_G value in the datasheet (1.78 kOhms). Further analysis may be required to ensure this does not affect results. 
- I am unsure what I should connect to the V-(in) pin and the Vo pin. I know that Vo is the output voltage, so I am thinking I should connect the Analog Discovery's scope channel 2 positive (blue) to it as it will measure the output. For V-(in) pin I am thinking I might connect the Analog Discovery's Wave Generator 2 to it; however, I am a bit unsure about doing this because I would need two different inputs. I will think about this a bit further before proceeding to the next steps.



Version 2.0 (10/05/22) - Rochelle De Silva
----------------------
- A Instrumentation Amplifier circuit is built utilizing a INA126PA amplifier. There is a positive supply voltage (red lead) of 5V and a negative supply voltage of -5 V (white lead) from the Analog Discovery. For the test signal (sine wave), there is voltage of 50 mV given to the circuit from the Waveform Generator 1 lead (yellow) as this is on the magnitude of a EOG signal.

- In Version 1.0, a resistance value of 1.882 kOhms (R_G) was actually utilized to connect to the gain setting pin, however this is the wrong resistance value for a gain of 50 (human error due to reading the wrong resistance value on the resistor). A resistance value R_G of 1.8 kOhm is utilized instead of the previous 1.882 kOhms resistance as the recommended resistance value to connect to the gain pins (R_G) is 1.78 kOhm. Although the R_G value used is 0.02 kOhms off from the recommended R_G value in the datasheet for INA126PA, the expected output should not change drastically and this error will be taken into account for further analysis. 

- The V-(in) pin is connected to ground for simulating the circuit with the test signal (sine wave). 

- The Vo pin is connected to the Analog Discovery's scope channel 2 positive (blue) to measure the output.

- The circuit with the 1.882 kOhm resistor can be found in the image **InstrumentationAmplifier_Circuit_1882_Ohm_Resistor.jpeg**. 

- The new circuit with the 1.8 kOhm resistor can be found in the images **InstrumentationAmplifier_Circuit_1800_Ohm_Resistor_1** & **InstrumentationAmplifier_Circuit_1800_Ohm_Resistor_2**.

Added to Circuit directory:
- InstrumentationAmplifier_Circuit_1882_Ohm_Resistor.jpeg
- InstrumentationAmplifier_Circuit_1800_Ohm_Resistor_1.jpeg
- InstrumentationAmplifier_Circuit_1800_Ohm_Resistor_2.jpeg

Known Problems:
- Circuit may need to be adapted so that the resistance is exactly 1.78 kOhms instead of 1.8 kOhms.
- Eventually when using a real EOG signal, the Vin(-) and Vin(+) pins which input the signal must be connected to two different electrodes and the signals coming in from those electrodes. Additionally the ground (Ref) pin must be connected to the third electrode which acts as the ground. The Vo pin will be connected to the next steps in the circuit such as further filtering.
- The signal inputted into the amplifier must also be filtered in a previous step. 


Version 3.0 (10/05/22) - Rochelle De Silva
----------------------
- For the Instruemntation Amplifier, a sine wave is utilized as a test signal. A 1 kHz Frequency and an amplitude of 1 V is utilized for the test signal in Waveforms' Wavegen. Originally, a amplitude of 1 V was utilized for the test signal, but this was too large, so the amplitude was changed to be on the magnitude of that of an EOG signal which is ~0-100 mV.

- The Scope in Waveforms displayed a strange output where the scope measuring the output of the amplifier generated a square wave. This is likely due to the fact that the input sine wave signal is getting clipped once it hits +/- 5V, resulting in it appearing as a square wave. This is not as expected. Further troubleshooting must be conducted to figure out why this is occuring.

- From the Network Analyzer in Waveforms, the gain is found to be 47.7529 instead of the expect 50. This was found by obtaining the DC gain in dB from the Network Analyzer output which was found to be 33.58 dB and converting it into voltage gain (47.7529) (which is unitless). The following equation is utilized and rearranged for gain: 33.58 dB = 20log(gain).

- Waveforms' in-progress Scope for the sine wave test signal input can be found in image **Instrumentation_Amplifier_InProgressScope_Sine_Input.png**.
- Waveforms' in-progress Network Analyzer bode plot can be found in image **Instrumentation_Amplifier_InProgressNetwork_Sine_Input.png**.

Added to Waveforms Input directory:
- Instrumentation_Amplifier_InProgressScope_Sine_Input.png
- Instrumentation_Amplifier_InProgressNetwork_Sine_Input.png

Known Problems:
- The output of the amplifier appears to output a clipped sine wave signal in Waveforms' Scope. As mentioned above, this is not as expected, and further troubleshooting must be conducted to figure out why this is occuring.
- From the Network Analyzer in Waveforms, the gain is found to be 47.7529 instead of the expected 50. This is slightly off, and I must conduct further troubleshooting to figure out why the gain might be slightly less than the expected gain of 50.
- The Network Analyzer frequency response output looks slightly off in general - there is a bit of noise, and the frequency response is not flat which is what would be expected without filtering and with using a test signal (sine wave).


Version 4.0 (10/05/22) - Rochelle De Silva
----------------------
- For the Instruemntation Amplifier, a sine wave is utilized as a test signal. A 1 kHz Frequency and an amplitude of 50 mV is utilized for the test signal in Waveforms' Wavegen. Originally, a amplitude of 1 V was utilized for the test signal, but this was too large, so the amplitude was changed to be on the magnitude of that of an EOG signal which is ~0-100 mV.

- From Version 3.0, it was discovered that the resistance in the circuit was wrong for a gain of 50 (human error due to reading the wrong resistance value on the resistor). This was fixed by utilizing a resistance of 1.8 kOhms instead of 1.882 kOhms. 

- From the Network Analyzer in Waveforms, the gain is found to be 49.6021 which is very close to the expect gain of 50. This was found by obtaining the DC gain in dB from the Network Analyzer output which was found to be 33.91 dB and converting it into voltage gain (49.6021) (which is unitless). The following equation is utilized and rearranged for gain: 33.91 dB = 20log(gain). The gain found is slightly smaller than the expected gain of 50 because a resistance of 1.8 kOhm is utilized in the circuit instead of the recommended 1.78 kOhm resistance (from the datasheet).

- Waveforms' Network Analyzer bode plot for the circuit with the 1.882 kOhm resistance (wrong resistance) can be found in image **WRONG_RESISTANCE_Instrumentation_Amplifier_Network_Sine_Input.png**.
- Waveforms' Wavegen sine wave test signal inputs can be found in image **Instrumentation_Amplifier_Wavegen_Sine_Input.png**.
- Waveforms' Scope for the sine wave test signal input can be found in image **Instrumentation_Amplifier_Scope_Sine_Input.png**.
- Waveforms' Network Analyzer bode plot for the circuit with 1.8 kOhm resistance can be found in image **Instrumentation_Amplifier_Network_Sine_Input.png**.

Added to Waveforms Input directory:
- WRONG_RESISTANCE_Instrumentation_Amplifier_Network_Sine_Input.png
- Instrumentation_Amplifier_Wavegen_Sine_Input.png
- Instrumentation_Amplifier_Scope_Sine_Input.png
- Instrumentation_Amplifier_Network_Sine_Input.png

Known Problems:
- The circuit may need to be adapted so that the resistance is exactly 1.78 kOhms instead of 1.8 kOhms, and this may change the frequency response and the gain (causing the gain to be closer, if not exactly, 50).
- Eventually when using a real EOG signal, the signal from electrodes will be inputted into the circuit. This will change the frequency response and 
- The signal inputted into the amplifier must also be filtered in a previous step which may also change the frequency response. A steeper roll-off is expected, with a roll-off per decade of around 20 (for first order filter). 
