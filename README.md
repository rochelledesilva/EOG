# EOG by Rochelle De Silva
Filter: 
-------------------------
**Rochelle De Silva (914561)**

High Pass and Low pass filters are simulated and built to filter the EOG signal. A high pass filter is utilized to attenuate/remove the DC offset from the signal. A low pass filter is utilized to remove high frequency noise which is outside the frequency range for an EOG signal of 0-40Hz. High frequencies such as powerline noise (50Hz) can interfere with the signal, and it is thus important to ensure that the noise at those higher frequencies is attenuated. In this stage of the EOG project, a circuit for the high pass filter is utilized as the first stage after capturing the EOG signal. After this signal is high-pass filtered, the signal is then passed through the Instrumentation Amplifier (built in a previous step of the EOG project) and then the output is passed through the low-pass filter to attenuate high frequency noise. It is essential that the signal is high-pass filtered before it is amplified because otherwise the DC offset will be amplified.

A notch filter assists in removing the 50 Hz powerline noise from the signal, which may interfere and create noise in the signal even after low-pass filtering.

The aim is to:
- Simulate and build high and low pass filter circuits in both LTSpice & WaveForms
- Test the high and low pass filters with a sine wave test signal
- Test the high and low pass filters with recorded EOG signal data
- Test the high and low pass filters with real time EOG signal data

Note that each directory contains files/uploads logged into a **changelog.md** file which contains details on each version in conjunction with the **README.md** file
