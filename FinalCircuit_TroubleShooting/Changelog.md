Change log for TroubleShooting Final Circuit
=======================================

Version 1.0 (27/05/22) - Rochelle De Silva
----------------------

The final circuit is built and tested with a sine wave test signal, a clean EOG test signal, a noisy EOG test signal, and a live EOG signal.

An in-progression version of the final circuit design can be found in images **NOTWORKING_Final_EOG_Circuit1.jpg**, **NOTWORKING_Final_EOG_Circuit2.jpg**, & **NOTWORKING_Final_EOG_Circuit3.jpg**. This circuit design did not work very well. There were a few issues that were uncovered after troubleshooting today. 

Firstly I tested out a sine wave test signal as displayed in image **FinalEog_Circuit_SineTestSignal_Wavegen.png**. The scope output of this test signal after the Instrumentation Amplifier and the comparator looked like it was working well, as found in images **FinalEog_Circuit_SineTestSignal_Scope_Amplifier.png** & **FinalEog_Circuit_SineTestSignal_Scope_Comparator.png** respectively. The peaks in the sinewave were detected and the signal was being amplified.

After this sine wave test signal, I decided to test a clean EOG test signal. I input the clean EOG test signal into Waveforms Wavegen as seen in image **Final_Circuit_CleanEOG_WavegenInput.png**. I then found the scope output of the negative peak detector (as seen in blue in image **Final_Circuit_CleanEOG_ScopeOutput_NegativePeakDetector.png**) and the scope output of the positive comparator (as seen in blue in image **Final_Circuit_CleanEOG_ScopeOutput_PositiveComparator.png**) with the scope input of the test sine wave (in yellow in both images). From these scope outputs, the circuit seems to handle the sine wave test signal well, detecting the peaks well and outputting a LED flash when peaks are detected. Overall the circuit seemed to work well with the clean EOG signal, so I decided to test the circuit with the noisy EOG signal.

I input the noisy EOG test signal into Waveforms Wavegen as seen in image **FinalCircuit_Noisy_EOG_Signal_WavegenInput.png**. I then scoped the peak detector (in blue) with the input noisy EOG test signal (in yellow) as seen in image **FinalCircuit_NoisyEOG_ScopeOutput_PeakDetector.png**. While the peak detector picked up on the peaks in the signal, the signal was still very noisy despite being passed through both the first order High and Low pass active filters. I then utilized the FFT function on the scope in Waveforms to see where the noise might be occurring in the signal and at what frequency, as seen in image **FinalCircuit_NoisyEOG_ScopeOutput_50HzNoise.png**. From this, I discovered that there was still a 50Hz powerline frequency noise in my signal which had not been attenuated through the first order Low Pass Active Filter. I then decided to add in my notch filter which attenuates the 50 Hz powerline frequency noise. The NetworkAnalyzer of the signal after both the first order Low Pass Active Filter and the Notch filter can be seen in image **FinalCircuit_LowPassNotch_NetworkAnalyzer.png**. From the Bode plot, it can be seen that the filters successfully attenuate the 50Hz powerline noise and also attenuates the signal after 40 Hz frequency.

I then decided to test a live EOG signal by connecting the electrodes to myself and the breadboard. When I connected the electrodes, there was no signal coming through the circuit from my eye movement. This can be seen in images **FinalCircuit_EOGSignal_Scope_NoOutput1.png** & **FinalCircuit_EOGSignal_Scope_NoOutput2.png**. However, I did notice that the 50 Hz powerline frequency was attenuated, displaying how the notch filter works well, as seen in image **FinalCircuit_EOGSignal_Scope_attenuated50Hz.png**.

During troubleshooting, I connected the electrodes directly to the Instrumentation Amplifier inputs instead of filtering them through the first order High Pass Active Filters first. I discovered that the EOG signal from  my eye movement was able to pass through the circuit, and resulted in the scopes picking up when I moved my eye horizontally. 

I then decided to change the order of my filters so that the order was Instrumentation Amplifier first, then a first order High Pass Active filter, then a Low Pass Active Filter and then my peak detectors and comparators.

The circuit thus successfully worked, detecting horizontal eyemovement really well. The final proof of a working device videos, scope outputs in Waveforms, and the final EOG circuit can be found in the Master Branch under the **Proof_of_Working_Device** & **Final EOG Circuit** directories.

Added to InProgress_FinalCircuit directory:
- NOTWORKING_Final_EOG_Circuit1.jpg
- NOTWORKING_Final_EOG_Circuit2.jpg
- NOTWORKING_Final_EOG_Circuit3.jpg

Added to TestSignal_SineWave directory:
- FinalEog_Circuit_SineTestSignal_Wavegen.png
- FinalEog_Circuit_SineTestSignal_Scope_Amplifier.png
- FinalEog_Circuit_SineTestSignal_Scope_Comparator.png

Added to TestSignal_CleanEog directory:
- Final_Circuit_CleanEOG_WavegenInput.png
- Final_Circuit_CleanEOG_ScopeOutput_NegativePeakDetector.png
- Final_Circuit_CleanEOG_ScopeOutput_PositiveComparator.png

Added to TestSignal_NoisyEOG directory:
- FinalCircuit_Noisy_EOG_Signal_WavegenInput.png
- FinalCircuit_NoisyEOG_ScopeOutput_PeakDetector.png
- FinalCircuit_NoisyEOG_ScopeOutput_50HzNoise.png
- FinalCircuit_LowPassNotch_NetworkAnalyzer.png

Added to TestSignal_NoisyEOG directory:
- FinalCircuit_EOGSignal_Scope_NoOutput1.png
- FinalCircuit_EOGSignal_Scope_NoOutput2.png
- FinalCircuit_EOGSignal_Scope_attenuated50Hz.png

