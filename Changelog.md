Change log for Peak Detector
=======================================

Positive Peak Detector
=======================================

Version 1.0 (20/05/22) - Rochelle De Silva
----------------------------------------------------
- I decided to utilize a positive peak detector as a rectifier to split the signal and only allow the positive signal to go through. This is done through a single diode and a capacitor. As the signal or voltage is supplied to the circuit from the voltage source, the diode is conducting the positive half of the signal to charge the capacitor with the positive input. For any negative voltage, the diode is not conducting, and results in an open circuit (since the diode is not conducting the negative signal), so it essentially becomes an RC circuit where current and charges are going to ground.

- I designed a basic positive peak detector utilizing a diode and a LM324N op-amp, and I simulated and tested this peak detector circuit with a sine wave test signal. I utilized the same circuit from Workshop 10 and decided to use different capacitor and resistor values to ensure that it would detect EOG signal peaks.

- I simulated a few different combinations of resistor and capacitor values in LTSpice. First, I simulated a positive peak detector circuit with an even voltage division, both resistors being 100kOhm, and with varying capacitor values of 1uF, 10 uF, 100uF, and 1000uF. These can be found in images **Positive_PeakDetector_1uF_100kOhm.png**, **Positive_PeakDetector_10uF_100kOhm.png**, **Positive_PeakDetector_100uF_100kOhm.png**, & **Positive_PeakDetector_1000uF_100kOhm.png** respectively. During these simulations it can be seen that with increasing capacitance, the capacitor takes longer to discharge after it has been charged from a positive peak in the voltage. 

- The voltage division across the resistors is also varied and simulated in LTSpice. A voltage division of two-thirds is simulated in LTSpice with varying capacitance values of 100uF and 1000uF. These can be found in images **Positive_PeakDetector_100uF_50kOhm_100kOhm.png** & **Positive_PeakDetector_1000uF_50kOhm_100kOhm.png** respectively.

- Based on this, varying capacitance will be changed when building and testing the circuit in Waveforms with the EOG test signal to ensure that the capacitor does not discharge so fast that it picks up smaller peaks in the EOG data from noise rather than actual eye movement. Thus a larger capacitance must be chosen to ensure that the rolloff isn't as steep. Additionally, the capacitor value cannot be so large that smaller peaks due to eye movement are not detected because the capacitor is too slow at discharging. A fine balance must be struck essentially between discharge of capacitor and the peaks due to eye movement that need to be detected. This needs to be further investigated when building and testing the circuit in Waveforms. I know that this will be the most challenging part because it will require switching resistor and capacitor values often until something works.

- Additionally, by varying the voltage division, the threshold for detecting a peak is changed. The threshold and the capacitance values will also need to be further investigated when building and testing the circuit in Waveforms. 

- The simulation of the basic positive peak detector for various combinations can be found in the images added to the LTSpice Simulation directory. 

Added to LTSpice Simulation directory:
- Positive_PeakDetector_1uF_100kOhm.png
- Positive_PeakDetector_10uF_100kOhm.png
- Positive_PeakDetector_100uF_100kOhm.png
- Positive_PeakDetector_1000uF_100kOhm.png
- Positive_PeakDetector_100uF_50kOhm_100kOhm.png
- Positive_PeakDetector_1000uF_50kOhm_100kOhm.png

Known Problems:
- The basic positive peak detector needs to be built on breadboards. 
- Various capacitor and resistor values must be tested (the same as those simulated in LTSpice).
- The build circuit will need to be tested and analyzed in Waveforms to see if the built circuit works. 
- Additionally, the peak detector will need to be tested with both a test signal (sine wave) and the clean and noisy EOG test signals to ensure that it will work well in detecting the right peaks in biological data from eye movement.
- A comparator must also be built which this basic postive peak detector outputs into, with the comparator causing an LED to flash when there is a peak in the positive signal.

Version 2.0 (21/05/22) - Rochelle De Silva
------------------------------------------------
- I built a basic positive peak detector utilizing a diode and a LM324N op-amp, and this peak detector circuit is tested with a sine wave test signal in Waveforms. There is a positive supply voltage (red lead) of 5V and a negative supply voltage of -5 V (white lead) from the Analog Discovery.

- The basic positive peak detector built circuit can be found in images **Positive_PeakDetector_Circuit1.jpg** & **Positive_PeakDetector_Circuit2.jpg**.

- I built the circuit with a 100uF capacitor and two 100kOhm resistors. I chose the values for the capacitor and resistors because a 100uF capacitor does not discharge as fast as the 1uF and 10uF capacitors, and slightly faster than a 1000uF, making it a good middle ground for detecting positive peaks in the signal. The two 100kOhm resistors were chosen as a starting point before testing out varying resistor values to cause a voltage division. However, after testing out the 100uF capacitor and two 100kOhm resistors and, the circuit worked well with both a sine test wave input (as seen in image **Positive_PeakDetector_Waveforms_100uF_100kOhm.png**)and the clean EOG signal (as seen in image **Positive_PeakDetector_Waveforms_ScopeOutput_CleanEOGSignal.png**) in Waveforms. 

- The circuit detected the positive peaks really well, whilst not picking up any smaller positive peaks which may be due to noise in the signal. Thus it was decided to keep the values as they were rather than changing them. I was pleasantly surprised that this circuit worked so well with the EOG data. 

Added to Circuit directory:
- Positive_PeakDetector_Circuit1.jpg
- Positive_PeakDetector_Circuit2.jpg

Added to Waveforms Input directory:
- Positive_PeakDetector_Waveforms_100uF_100kOhm.png
- Positive_PeakDetector_Waveforms_ScopeOutput_CleanEOGSignal.png

Known Problems:
- The circuit still needs to be tested with the noisy EOG signal to ensure that the positive peaks are picked up accurately. However, this might need to be done once the signal is passed through the rest of the circuit (high-pass filtered, amplified, low-pass filtered) because I want to ensure that the peak detector works well with the rest of the circuit with the noisy test data, rather than just by itself.
- A positive comparator needs to be built and added to the circuit, causing an LED to turn on whenever there is a positive peak detected.

Version 3.0 (22/05/22) - Positive Comparator - Rochelle De Silva
------------------------------------------------
- I built a positive comparator circuit. This circuit inputs the positive peak detector output and will output a square waveform which will 
result in an LED display. The LED will switch on when a peak is detected, and the comparator outputs a 1. The LED will switch off when there is no peak detected, and the comparator outputs a 0.

- This positive comparator circuit built after the positive peak detector is simulated in LTSpice. When I simulated it in LTSpice, I found that I accidentally placed the inputs from the positive peak detector and the signal from the voltage source into the wrong pins. There are two inputs to the comparator V_i and V_ob. V_i is in the input from the voltage source, and V_ob is the input from the peak detector output. I accidentally put the output for V_ob on the wrong pin of the comparator and this resulted in a square wave that detected the negative peak in the sine wave, as seen in image **Positive_PeakComparator_LTSpice_Simulation_WrongComparatorInputPins.png**. I thus switched the inputs to the pins so that the square wave would output a 1 when there is a positive peak as seen in image **Positive_PeakComparator_LTSpice_Simulation.png**. 

- The simulations worked really well in LTSpice so I decided to move onto building the circuit, since it seemed really simple. At first, I tried using a LM324N op-amp as the comparator because the symbols look very similar in the circuit; however, I soon after got very confused because I didn't understand where to put the inputs/outputs, and how exactly the op-amp would become a comparator. I then realized that I had gone about building the circuit wrong and should not have been using a LM324N op-amp for it. I then realized that the LM339 is utilized as a comparator in the circuit, and I switched it out.

- I thus utilized a LM339 as a comparator in the circuit.  This circuit can be found in image **Circuit_PositivePeakComparator_NegativePeakComparator1.jpg** & **Circuit_PositivePeakComparator_NegativePeakComparator2.jpg**. I built both the positive and negative peak comparators at the same time, so the images contain them jointly combined and inputted/outputted through the LM339. 

- I then tested the circuit in Waveforms to ensure that it was working properly and detected the positive signal well. I decided to test out the Clean EOG signal since I had already tested the positive peak detector with a sine test wave a few days ago, and it was working well. The Waveforms Scope output can be found in images **Positive_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal.png** & **Positive_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal2.png**. As can be seen from the images, the peaks are detected quite well, and a square wave is outputted at each positive peak. For some reason the square wave is upside down, which I could not figure out why, but I will have a further think about how to fix that later.

- A green LED is successfully switched on whenever a positive peak is detected, and switched off for the scenarios where there is no peak or a negaitve peak.

Added to LTSpice Simulation directory:
- Positive_PeakComparator_LTSpice_Simulation.png
- Positive_PeakComparator_LTSpice_Simulation_WrongComparatorInputPins.png

Added to Circuit directory:
- Circuit_PositivePeakComparator_NegativePeakComparator1.jpg
- Circuit_PositivePeakComparator_NegativePeakComparator2.jpg

Added to Waveforms Input directory:
- Positive_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal.png
- Positive_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal2.png

Known Problems:
- The square wave output from the comparator is upside down. I'm unsure why this might be. Potentially because I flipped the positive and negative inputs on the LM339. I will need to further investigate this. However, the comparator still works regardless, so this is a minor issue.
- The positive peak detector and comparator will need to be connected to the rest of the circuit (with the High and low pass filters and the amplifier). Additionally, a noisy EOG signal will need to be tested with the circuit.


Negative Peak Detector
=======================================

Version 1.0 (20/05/22) - Rochelle De Silva
----------------------------------------------------------
- I utilized a negative peak detector as a rectifier to split the signal and only allow the negative signal to go through. This is done through a single diode and a capacitor. As the signal or voltage is supplied to the circuit from the voltage source, a diode (which is flipped in orientation in the circuit) is conducting the negative half of the signal to charge the capacitor with the negative input. For any positive voltage, the diode is not conducting, and results in an open circuit (since the diode is not conducting the positive signal), so it essentially becomes an RC circuit where current and charges are going to ground.

- I designed a basic negative peak detector utilizing a diode (flipped in orientation) and a LM324N op-amp, and I then simulated and tested this peak detector circuit with a sine wave test signal. I utilized the same circuit from Workshop 10, however I flipped the orientation of the diode so that it could detect the negative signals. I also decided to use different capacitor and resistor values to ensure that it would detect EOG signal peaks.

- I simulated a few different combinations of resistor and capacitor values in LTSpice. First, I simulated a negative peak detector circuit with an even voltage division, both resistors being 100kOhm, and with varying capacitor values of 1uF, 10 uF, 100uF, and 1000uF. These can be found in images **Negative_PeakDetector_1uF_100kOhm.png**, **Negative_PeakDetector_10uF_100kOhm.png**, **Negative_PeakDetector_100uF_100kOhm.png**, & **Negative_PeakDetector_1000uF_100kOhm.png** respectively. During these simulations it can be seen that with increasing capacitance, the capacitor takes longer to discharge after it has been charged from a negative peak in the voltage. 

- I also varied and simulated the voltage division across the resistors in LTSpice. I simulated a voltage division of one-third and two-thirds in LTSpice with the same capacitance of 100uF. These can be found in images **Negative_PeakDetector_100uF_Voltage_Divison_1third_100kOhm_50kOhm.png** & **Negative_PeakDetector_100uF_Voltage_Divison_2thirds_100kOhm_50kOhm.png** respectively. 

- Like with the positive peak detector, based on this, varying capacitance will be changed when building and testing the circuit in Waveforms with the EOG test signal to ensure that the capacitor does not discharge so fast that it picks up smaller peaks in the EOG data from noise rather than actual eye movement. Thus a larger capacitance must be chosen to ensure that the rolloff isn't as steep. Additionally, the capacitor value cannot be so large that smaller peaks due to eye movement are not detected because the capacitor is too slow at discharging. A fine balance must be struck essentially between discharge of capacitor and the peaks due to eye movement that need to be detected. This needs to be further investigated when building and testing the circuit in Waveforms. I know that this will be the most challenging part because it will require switching resistor and capacitor values often until something works.

- Additionally, by varying the voltage division, the threshold for detecting a peak is changed. The threshold and the capacitance values will also need to be further investigated when building and testing the circuit in Waveforms. The one-third voltage division seemed to be too low a threshold, so a two-thirds threshold will be further investigated.

- The simulation of the basic negative peak detector for various combinations can be found in the images added to the LTSpice Simulation directory. 

Added to LTSpice Simulation directory:
- Negative_PeakDetector_1uF_100kOhm.png
- Negative_PeakDetector_10uF_100kOhm.png
- Negative_PeakDetector_100uF_100kOhm.png
- Negative_PeakDetector_1000uF_100kOhm.png
- Negative_PeakDetector_100uF_Voltage_Divison_1third_100kOhm_50kOhm.png
- Negative_PeakDetector_100uF_Voltage_Divison_2thirds_100kOhm_50kOhm.png

Known Problems:
- The basic negative peak detector needs to be built on breadboards.
- The build circuit will need to be tested and analyzed in Waveforms to see if the built circuit works. 
- Additionally, the peak detector will need to be tested with both a test signal (sine wave) and the clean and noisy EOG test signals to ensure that it will work well in detecting the right peaks in biological data from eye movement.
- A comparator must also be built which this basic negative peak detector outputs into, with the comparator causing an LED to flash when there is a peak in the negative signal.


Version 2.0 (21/05/22) - Rochelle De Silva
------------------------------------------------
- I built a basic negative peak detector utilizing a diode (in reverse direction) and a LM324N op-amp, and I tested this peak detector circuit with a sine wave test signal in Waveforms. There is a positive supply voltage (red lead) of 5V and a negative supply voltage of -5 V (white lead) from the Analog Discovery.

- The basic negative peak detector built circuit can be found in images **Negative_PeakDetector_Circuit1.jpg** & **Negative_PeakDetector_Circuit2.jpg**.

- I first built the circuit with a 100uF capacitor and two 100kOhm resistors. I chose the values for the capacitor and resistors because a 100uF capacitor does not discharge as fast as the 1uF and 10uF capacitors, and slightly faster than a 1000uF, making it a good middle ground for detecting negative peaks in the signal. The 100kOhm resistors were chosen as a starting point before unequal voltage division between the resistors is explored in Waveforms. The Wavegen input and Scope output can be found in images **Negative_PeakDetector_Waveforms_ScopeOutput_SineTestSignal.png** & **Negative_PeakDetector_Waveforms_WavegenInput_SineTestSignal.png** respectively. The circuit worked well with the sine test wave input, so I decided to try out varying the voltage division whilst 

- I then built the circuit with a 100uF capacitor and a two-thirds voltage division with one 50kOhm resistor and one 100kOhm resistor. I tested the circuit with the clean EOG test signal in Waveforms, and the Wavegen input and Scope output can be found in images **Negative_PeakDetector_Waveforms_ScopeOutput_SineTestSignal.png** & **Negative_PeakDetector_Waveforms_WavegenInput_SineTestSignal.png** respectively. The circuit worked well with the sine test wave input, so I decided to test it the circuit with the clean EOG test signal data.

- Upon uploading the clean EOG signal data into Waveforms Wavegen, two issues occurred. First, I did not realize there was a sample rate for the clean EOG test signal data, so I uploaded it with the automated 1kHz sample rate as seen in image **ISSUE_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_1kHzSampleRate.png**. However, I realized that the excel sheet for the EOG data had recommended a 256 Hz sampling rate for the data, so I changed it as seen in image **ISSUE_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_256HzSampleRate.png**.

- The other issue I encountered was that the amplitude which was input into Wavegen was too large compared to the amplitude of an EOG signal which is around 50 mV. I thus changed the amplitude to 50 mV in Wavegen as displayed in image **ISSUES_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_50mV.png**.

- I then tested the circuit with the clean EOG signal. As can be seen from image **Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal.png**, the negative peak detector does quite a good job at detecting the negative peaks; however, there are some issues where it seems to be detecting smaller negative peaks which could potentially be due to noise. Thus I decided to test different capacitor values with a two-thirds voltage division of 50kOhm and 100kOhm resistors. 

- First I tested a 100uF capacitor with the two-thirds voltage division as found in image **Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal_100uF_50kOhm_100kOhm.png**. The voltage division and capacitance value seemed to help with detecting the larger negative peaks; however, there were still some smaller negative peaks that were getting picked up by the detector despite the fact that those peaks could just be due to noise. Thus, I increased the capacitance to 220uF as seen in image **Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal_220uF_50kOhm_100kOhm.png**. This however, seemed to cause the opposite effect, missing a lot of the negative peaks which were likely due to eye movement rather than noise. 

- Further investigation must be conducted to find the optimal capacitor value for the negative peak detector.

Added to Circuit directory:
- Negative_PeakDetector_Circuit1.jpg
- Negative_PeakDetector_Circuit2.jpg

Added to Waveforms Input directory:
- Negative_PeakDetector_Waveforms_ScopeOutput_SineTestSignal.png
- Negative_PeakDetector_Waveforms_WavegenInput_SineTestSignal.png
- Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal.png
- Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal.png
- Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal_100uF_50kOhm_100kOhm.png
- Negative_PeakDetector_Waveforms_ScopeOutput_CleanEogSignal_220uF_50kOhm_100kOhm.png
- ISSUE_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_1kHzSampleRate.png
- ISSUE_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_256HzSampleRate.png
- ISSUES_Negative_PeakDetector_Waveforms_WavegenInput_CleanEogSignal_50mV.png

Known Problems:
- At the moment, the capacitance values either miss importance negative peaks in the signal, or pick up the smaller, less signficiant peaks in the data which could be due to noise. 
- Thus, further investigation needs to be conducted to find the optimal capacitance value that picks up the major negative peaks in the Clean EOG test data.
- The circuit still needs to be tested with the noisy EOG signal to ensure that the negative peaks are picked up accurately. However, this might need to be done once the signal is passed through the rest of the circuit (high-pass filtered, amplified, low-pass filtered) because I want to ensure that the peak detector works well with the rest of the circuit with the noisy test data, rather than just by itself.
- A negative comparator needs to be built and added to the circuit, causing an LED to turn on whenever there is a negative peak detected.

Version 4.0 (22/05/22) - Negative Comparator - Rochelle De Silva
------------------------------------------------
- I built a negative comparator circuit. This circuit inputs the negative peak detector output and will output a square waveform which will 
result in an LED display. The LED will switch on when a peak is detected, and the comparator outputs a 1. The LED will switch off when there is no peak detected, and the comparator outputs a 0.

- This negative comparator circuit built after the negative peak detector is simulated in LTSpice, and this simulation can be found in the image **Negative_PeakComparator_LTSpice_Simulation.png**.

- The simulations worked really well in LTSpice so I decided to move onto building the circuit, since it seemed really simple. I utilized the same LM339 as the positive comparator in the circuit. I then put a blue LED on the output of the circuit for the LED display.

- This circuit can be found in image **Circuit_PositivePeakComparator_NegativePeakComparator1.jpg** & **Circuit_PositivePeakComparator_NegativePeakComparator2.jpg**. I built both the positive and negative peak comparators at the same time, so the images contain them jointly combined and inputted/outputted through the LM339. 

- I then tested the circuit in Waveforms to ensure that it was working properly and detected the negative signal well. I decided to test out the Clean EOG signal since I had already tested the negative peak detector with a sine test wave and the Clean EOG signal, and it was working well. I decided to change out the capacitor values to try to optimize the negative peak detection in the circuit. I tested 133uF, 136.3uF, 137.7uF, and 147uF capacitors. The Waveforms Scope output can be found in images **Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_133uF.png**, **Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_136.3uF.png**, **Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_137.7uF.png**, & **Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_147uF.png** respectively. 

- The negative comparator results in a square wave is outputted at each negative peak. As can be seen from the images, the negative peaks are most optimally detected with a 136.3uF capacitor. For lower capacitor values, too many smaller negative peaks are detected, and for higher capacitor values, only the largest negative peaks are detected. Thus a 136.3uF capacitor provides a middle ground for optimally detecting most of the prominent negative peaks likely due to eye movement.

- A blue LED is successfully switched on whenever a negative peak is detected, and switched off for the scenarios where there is no peak or a positive peak.

Added to LTSpice Simulation directory:
- Negative_PeakComparator_LTSpice_Simulation.png

Added to Circuit directory:
- Circuit_PositivePeakComparator_NegativePeakComparator1.jpg
- Circuit_PositivePeakComparator_NegativePeakComparator2.jpg

Added to Waveforms Input directory:
- Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_133uF.png
- Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_136.3uF.png
- Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_137.7uF.png
- Negative_PeakComparator_Waveforms_ScopeOutput_CleanEOGSignal_147uF.png

Known Problems:
- The capacitance value could be tweaked further to ensure optimal detection of negative peaks in the EOG data.
- The negative peak detector and comparator will need to be connected to the rest of the circuit (with the High and low pass filters and the amplifier). Additionally, a noisy EOG signal will need to be tested with the circuit.
