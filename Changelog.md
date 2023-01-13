Change log for Filter
=======================================

High Pass Filter
=======================================

Version 1.0 (12/05/22) - Sallen Key High Pass Filter -  Rochelle De Silva
----------------------------------------------------
- A Sallen Key High-Pass Active Filter is simulated in LTSpice. To ensure the simplicity of the filter, both capacitor values and resistor values are kept the same. 

- Resistor and capacitor values are found by utilizing the cut-off frequency equation of f_c = 1/(2*pi*R*C), noting that the cut-off frequency for the High-pass filter is f_c = 0.1 Hz, which ensures that the DC Offset is attenuated and removed. 

- Utilizing this cut-off frequency value of 0.1 Hz, a reasonable capacitor value such as 100uF is chosen and the resistor value is then found using the equation. The resistor value is 1.592kOhm. An image of this specific configuration of the High-Pass filter can be found in image **HighPass_SallenKeyActiveFilter_1.592kOhm.png**.

- I also tried a transient analysis on this circuit, and quickly realized that this did not provide too much information about the frequency response. An image of this atempt can be found in **HighPass_SallenKeyActiveFilter_TransientAnalysis.png**.

- I also decided to try a different capacitance value of 10uF. This resulted in a resistor value of 940 Ohm. An image of this specific configuration of the High-Pass filter can be found in image **HighPass_SallenKeyActiveFilter_940_Ohm.png**. This image displays the simulation of the Sallen Key High-Pass Active Filter in LTSpice. The cut-off frequency at -3dB is about 26 Hz. However, for this second order filter it is expected that the cutoff frequency should be around 0.1Hz. I am a bit unsure how to procede with this. I potentially made a mistake in my calculations or I may have used the equation for cut-off frequency wrong. I need to further investigate how to procede and any issues that may have arisen during this. Alternatively, I may try to build a simpler filter circuit. It might be a better method of building the EOG filters to start off with a simple filter (such as a basic passive or active filter) and then increase the complexity of the filter design.

Added to LTSpice Simulation directory:
- HighPass_SallenKeyActiveFilter_1.592kOhm.png
- HighPass_SallenKeyActiveFilter_940_Ohm.png
- HighPass_SallenKeyActiveFilter_TransientAnalysis.png

Known Problems:
- It was difficult to get to the right cutoff frequency too because this was a second order high pass filter. Overall it was very difficult, and a hard filter to start out with.
- I also found it really difficult to build the Sallen Key High Pass Filter on a breadboard. I might try an easier filter to build such as a passive or active high-pass filter. This is because it might be a better method of building the high pass filter to start with a simpler filter first and then increase in complexity of the filter design.

Version 2.0 (15/05/22) - High Pass Passive Filter - Rochelle De Silva
------------------------------------------------
- I initially simulated a high pass passive filter in LTSpice. However, I decided that active filtering may be better than passive filtering because active filtering has many benefits over passive filtering including active filters are less susceptible to loading due to its high input impedance and very low output impedance, can include amplification if needed, and can maintain a filter response close to the ideal operation. 

Added to LTSpice Simulation directory:
- HighPass_PassiveFilter_LTSpice_Simulation.png

Known Problems:
- I aim to active filter the EOG signal instead of passive filtering because active filtering seems to have a few more advantages over passive filtering. . Although passive filtering is a completely viable alternative and option for filtering and attenuate the DC offset.

Version 3.0 (17/05/22) - High Pass Active Filter - Rochelle De Silva
------------------------------------------------
- I have chosen to build a first order High Pass Active filter because they are less susceptible to loading due to its high input impedance and very low output impedance, can include amplification if needed, and can maintain a filter response close to the ideal operation. The High Pass Active filter will be simulated and built with a LM324N op-amp in addition to RLC because the active filter needs power. 

- This high pass active filter is intended to remove/attenuate the DC offset from the incoming EOG signal, and does not require any amplification because I do not want to amplify the DC offset; thus, I have decided to ensure that the filter has a gain of 1 so that there is no amplification in the filter, and this results in the resistors being of equal value. 

- The cutoff frequency equation for the high pass active filter is f_c = 1/(2*pi*R*C). As DC offset needs to be removed, the f_c = 0.1 Hz. I chose a reasonable capacitor value of 1000uF which corresponds to a resistor value of R = 1591.5Ohm (obtained from rearranging the equation). I simulated this circuit in LTSpice with those capacitor and resistor values and this can be seen in image **HighPass_ActiveFilter_1.591KOhm.png**. From this image, the frequency response displays how at -3dB there is a cutoff frequency of 100mHz, as desired. Thus, as shown by this LTSpice simulation, this filter is working as intended. 

- It is difficult to get a resistor of the value 1.591kOhm, thus I decided to round the resistor value up to 1.6kOhm. I simulated this circuit in LTSpice with this new resistor value to ensure that the cutoff frequency did not change drastically, and this can be seen in image **HighPass_ActiveFilter_1.6KOhm.png**. From this image, the frequency response displays how at -3dB there is a cutoff frequency of 100mHz still, as desired. Thus, as shown by this LTSpice simulation, this filter with a rounded up resistor value is working as intended. 

Added to LTSpice Simulation directory:
- HighPass_ActiveFilter_1.591KOhm.png
- HighPass_ActiveFilter_1.6KOhm.png

Known Problems:
- The high-pass active filter simulated today still needs to be built and tested using Waveforms. 
- The high-pass active filter must be tested in Waveforms with both a sine wave test signal, a clean EOG signal, and a noisy EOG signal to ensure that it is working properly.

Version 4.0 (18/05/22) - High Pass Active Filter - Rochelle De Silva
------------------------------------------------
- I built the High Pass Active Filter that I designed and simulated yesterday in LTSpice. This built circuit can be found in images **HighPass_ActiveFilter_Circuit1.jpg** & **HighPass_ActiveFilter_Circuit2.jpg**. 

- I initially tried to test the High Pass Active Filter by inputting a sine wave of 50mV amplitude into Waveforms Wavegen as seen in image **ISSUE_HighPass_ActiveFilter_WavegenInput.png**. Additionally, I scoped the output which displayed that inverted sine waves (because the cutoff frequency equation utilized with a gain of 1 inverted the input) as seen in image **ISSUE_HighPass_ActiveFilter_ScopeOutput.png**.

- One issue I faced is observing the Bode plot of the High Pass Active Filter in the Network Analyzer of Waveforms. I waited over an hour for the plot to load, and tried it multiple times after that, but I was unsuccessful in viewing the actual plot as displayed in image **ISSUE_HighPass_ActiveFilter_NetworkAnalyzer.png**. Due to the Network Analyzer taking excessively long amount of time to load, I decided to test the working of the filter through alternative means. 

- I tested a DC input of 5V for the high-pass active filter as seen in image **HighPass_ActiveFilter_WavegenInput.png**. As seen from the scope in image **HighPass_ActiveFilter_ScopeOutput.png** this input is attenuated to 0V, which displays how the high-pass active filter is working correctly.

Added to Circuit directory:
- HighPass_ActiveFilter_Circuit1.jpg
- HighPass_ActiveFilter_Circuit2.jpg

Added to Waveforms Input directory:
- HighPass_ActiveFilter_WavegenInput.png
- HighPass_ActiveFilter_ScopeOutput.png
- ISSUE_HighPass_ActiveFilter_WavegenInput.png
- ISSUE_HighPass_ActiveFilter_ScopeOutput.png
- ISSUE_HighPass_ActiveFilter_NetworkAnalyzer.png

Known Problems:
- It is difficult to observe the Bode plot of the High Pass Active filter in the Network Analyzer of Waveforms because it takes an excessively long amount of time to load. Thus, the main indication that the high-pass active filter works is by testing a DC input of 5V. As seen from the scope this input is attenuated to 0V, which displays how the high-pass active filter is working correctly.


Low Pass Filter
=======================================

Version 1.0 (10/05/22) - Sallen Key Low Pass Active Filter - Rochelle De Silva
----------------------------------------------------------
- A Sallen Key Low-Pass Active Filter is simulated in LTSpice. To ensure the simplicity of the filter, both capacitor values and resistor values are kept the same. 

- Resistor and capacitor values are found by utilizing the cut-off frequency equation of f_c = 1/(2*pi*R*C), noting that the cut-off frequency for the Low-pass filter is f_c = 40 Hz, which is lower than the 50 Hz powerline frequency noise which needs to be attenuated. Utilizing this cut-off frequency value of 40 Hz, a reasonable capacitor value such as 100nF is chosen and the resistor value is then found using the equation. The resistor value is 39.789kOhm. 

- The Sallen Key Low-Pass Active Filter is simulated in LTSpice, as found in the file **LowPass_SallenKeyActiveFilter_39.7kOhm.pdf**.

- The cut-off frequency at -3dB is about 26 Hz. However, for this second order filter it is expected that the cutoff frequency should be around 40Hz. I am a bit unsure how to procede with this, considering I used the equation for cut-off frequency right. I need to further investigate how to procede. Alternatively, I may try to build a simpler filter circuit. It might be a better method of building the EOG filters to start off with a simple filter (such as a basic passive or active filter) and then increase the complexity of the filter design.

Added to LTSpice Simulation directory:
- LowPass_SallenKeyActiveFilter_39.7kOhm.pdf

Known Problems:
- It was difficult to get to the right cutoff frequency too because this was a second order low pass filter. Overall it was very difficult, and a hard filter to start out with.
- I also found it really difficult to build the Sallen Key Low Pass Filter on a breadboard. I might try an easier filter to build such as a passive or active low-pass filter. This is because it might be a better method of building the low pass filter to start with a simpler filter first and then increase in complexity of the filter design.

Version 2.0 (15/05/22) - Low Pass Passive Filter - Rochelle De Silva
------------------------------------------------
- I initially simulated a low pass passive filter in LTSpice. However, I decided that active filtering may be better than passive filtering because active filtering has many benefits over passive filtering including active filters are less susceptible to loading due to its high input impedance and very low output impedance, can include amplification if needed, and can maintain a filter response close to the ideal operation. 

Added to LTSpice Simulation directory:
- LowPass_PassiveFilter_LTSpice_Simulation.png

Known Problems:
- I aim to active filter the EOG signal instead of passive filtering because active filtering seems to have a few more advantages over passive filtering. Although passive filtering is a completely viable alternative and option for filtering and attenuate the high frequency noises.

Version 3.0 (17/05/22) - Low Pass Active Filter - Rochelle De Silva
------------------------------------------------
- I designed and simulated a first order Low Pass Active Filter. This filter is designed to attenuate the signal for frequencies greater than 40 Hz. This essentially will attenuate any noise from powerline noise (at 50Hz) and any other noise to ensure the clarity of the EOG signal which is under 40Hz. An EOG signal lies between 0-40Hz, so by low-pass filtering (after previously high-pass filtering and amplifying), should ensure that the signal is not attenuated and is within the desired frequency range. 

- Active filters require power and I thus decided to power the filter with a LM324N op-amp.

- As active filters can amplify the signal, for this specific EOG project, there is no need for amplification because the signal has been amplified in a previous step of the EOG utilizing an Instrumentation amplifier. The Low-Pass filter is thus filtering this amplified signal. Thus, a gain of 1 is implemented in this active low-pass filter design. This essentially results in the resistor values being the same. The resulting cut-off frequency equation is f_c = 1/(2*pi*R*C). Since the cutoff frequency is f_c = 40Hz, I tried various capacitor and resistor values which satisfy the cut-off frequency equation and are reasonable for building the circuit. This includes combinations of a 10uF capacitor with a 39.788Ohm resistor as seen in image **LowPass_ActiveFilter_39.7Ohm.png**, 10uF capacitor with a 397.887Ohm resistor as seen in image **LowPass_ActiveFilter_397Ohm.png**, and a 1uF capacitor with a 3.97kOhm resistor as seen in image **LowPass_ActiveFilter_3.9KOhm.png**. For the 39.788Ohm resistor with a 10uF capacitor, I had done the calculations wrong for the cut-off frequency, and realized that I should have been using a 397.887Ohm resistor. When simulated both circuit combinations for the 10uF and 1uF capacitors had 40Hz cutoff frequency at -3dB as expected.

- I decided that I wanted to use the 1uF capacitor with a 3.97kOhm resistor because they seem liked reasonable values and I have resistors that can add to 4kOhm. As 3.97kOhm is a difficult value of resistance to build in a circuit, I thus simulated a 4kOhm resistor with the 1uF capacitor in LTSpice to ensure that a roundedup resistor value would work well in the circuit. This simulation can be found in image **LowPass_ActiveFilter_4kOhm.png**. The cutoff frequency is 40Hz at -3dB as expected. Thus this filter works well when simulated. 


Added to LTSpice Simulation directory:
- LowPass_ActiveFilter_3.9KOhm.png
- LowPass_ActiveFilter_4kOhm.png
- LowPass_ActiveFilter_39.7Ohm.png
- LowPass_ActiveFilter_397Ohm.png

Known Problems:
- The low-pass active filter simulated today still needs to be built and tested using Waveforms. 
- The low-pass active filter must be tested in Waveforms with both a sine wave test signal, a clean EOG signal, and a noisy EOG signal to ensure that it is working properly.

Version 4.0 (18/05/22) - Low Pass Active Filter - Rochelle De Silva
------------------------------------------------
- I built the first order Low Pass Active Filter that I designed and simulated in LTSpice yesterday. The built circuit can be found in images **LowPass_ActiveFilter_Circuit1.jpg** & **LowPass_ActiveFilter_Circuit2.jpg**.

- I then tested the built circuit in Waveforms, however, I encountered an issue where the Network Analyzer in Waveforms had a strange output as seen in images **ISSUE_LowPass_ActiveFilter_NetworkAnalyzer1.png** & **ISSUE_LowPass_ActiveFilter_NetworkAnalyzer2.png**. The output displayed a bode plot that did not attenuate the signal after 40 Hz. Instead the signal appeared to get attenuated slightly before rising back up. This appeared like a reverse bandpass filter. I was very confused why this issue was occuring.

- After I troubleshooted for a while, I realized that my input amplitude into Network Analyzer was 1V which is too large for the EOG signal which is of amplitude 50 mV. I thus changed this setting, and ran the network analyzer again as displayed in images **LowPass_ActiveFilter_NetworkAnalyzer1.png** & **LowPass_ActiveFilter_NetworkAnalyzer2.png**. From these two images and the image **LowPass_ActiveFilter_NetworkAnalyzer3.png** it can be discerned that around 40 Hz, the signal is attenuated and has a -20dB/decade dropoff as expected for this first order filter.

- The filter appears to be working well, as expected

Added to Circuit directory:
- LowPass_ActiveFilter_Circuit1.jpg
- LowPass_ActiveFilter_Circuit2.jpg

Added to Waveforms Input directory:
- LowPass_ActiveFilter_NetworkAnalyzer1.png
- LowPass_ActiveFilter_NetworkAnalyzer2.png
- LowPass_ActiveFilter_NetworkAnalyzer3.png
- ISSUE_LowPass_ActiveFilter_NetworkAnalyzer1.png
- ISSUE_LowPass_ActiveFilter_NetworkAnalyzer2.png

Known Problems:
- The filter will need to be tested with the clean and noisy EOG signal. I will do this once the filter is added into the complete EOG circuit.

Notch Filter
=======================================
Version 1.0 (23/05/22) - Active Notch - Rochelle De Silva
-------------------------------------
- When the EOG circuit is run with a high-pass filter, instrumentation amplifier, low-pass filter, positive and negative peak detectors and comparators, the signal output in Waveforms appears noisy.
- It is difficult to remove the 50 Hz powerline interference noise from the signal with the current filters utilized. Thus, a notch filter is built in order to remove noise at the 50 Hz frequency.
- To build the Active Twin-T Notch Filter, I followed the circuit schematic from the following website: https://www.electronics-notes.com/articles/analogue_circuits/operational-amplifier-op-amp/notch-filter-active-circuit.php 
- On this website, it suggested capacitor and resistor values to attenuate the 50 Hz powerline noise requency. I thus utilized capacitor values of 47nF, R1 = R2 = 10kOhm, and R3 = R4 = 68kOhm resistor values. 
- This is simulated in LTSpice, as can be found in **Active_Notch_Filter_LTSpice_Simulation.png**.


Added to LTSpice Simulation directory:
- Active_Notch_Filter_LTSpice_Simulation.png

Known Problems:
- The notch filter does not attenuate the 50 Hz powerline noise frequency.
- It is really difficult to get values for the resistors and capacitors. I might need to change the values of them to ensure that the 50 Hz noise is attenuated. The website I followed may have not had accurate values for the Active Twin-T Notch Filter design. I need to do further research into this.


Version 2.0 (23/05/22) - Pasive Notch - Rochelle De Silva
-------------------------------------
- When the EOG circuit is run with a high-pass filter, instrumentation amplifier, low-pass filter, positive and negative peak detectors and comparators, the signal output in Waveforms appears noisy.
- It is difficult to remove the 50 Hz powerline interference noise from the signal with the current filters utilized. Thus, a notch filter is built in order to remove noise at the 50 Hz frequency.
- Based on the notch frequency equation for a Basic Twin-T Notch filter design, f_N = 1/(4*pi*R*C). Since f_N = 50 Hz, as the frequency selected for the notch to be attenuated is 50 Hz, combinations of resistor (R) and capacitor (C) values are found so satisfy this equation.
- A capacitor value of 100nF is chosen, and a corresponding resistor value of 15.951kOhm is found. Thus, two of the resistor values will be 31.831 kOhm (as in the circuit design it is 2R) and one resistor value is 15.951kOhm. This is simulated in LTSpice, as can be found in **Passive_Notch_Filter_LTSpice_Simulation_31.831kOhm.png**. 
- Since this resistor value is so specific, it is difficult to get that exact value in actuality, when building the circuit. Thus, the resistor value is rounded up to R = 16 kOhm. Thus, two of the resistor values will be 32 kOhm (as in the circuit design it is 2R) and one resistor value is 16kOhm. This is simulated in LTSpice, as can be found in **Passive_Notch_Filter_LTSpice_Simulation_32kOhm.png**. As can be discerned from the simulation, despite the estimation/rounding of the resistor value, a 50.11 Hz frequency is attenuated through the notch filter.
- A circuit is thus built utilizing 100nF capacitors, 16 kOhm and 32 kOhm resistors, and this can be found in **Passive_Notch_Filter_Circuit_32kOhm.jpg**.
- A Waveforms simulation of the built circuit is conducted utilizing a sine test signal, and this can be found in **Passive_Notch_Filter_Waveforms_32kOhm.png**.

Added to LTSpice Simulation directory:
- Passive_Notch_Filter_LTSpice_Simulation_31.831kOhm.png
- Passive_Notch_Filter_LTSpice_Simulation_32kOhm.png

Added to Circuit directory:
- Passive_Notch_Filter_Circuit_32kOhm.jpg

Added to Waveforms Input directory:
- Passive_Notch_Filter_Waveforms_32kOhm.png

Known Problems:
- I still need to test the output of the notch filter circuit in Waveforms using the EOG data individually.
- When adding in the Notch filter, the noise is still present in the overall signal so there may be other issues with the overall circuit.
