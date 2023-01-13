# EOG by Rochelle De Silva
**Rochelle De Silva (914561)**

How to navigate GitLab for my EOG project
-----------------------------------------
All uploads can be found in the **Repository** section of my GitLab. There are four main branches:

- Transistor Switch
- Amplifier
- Filter
- Peak Detector
- Master

Each of these branches contains multiple directories. Note that each directory contains files/uploads logged into a changelog.md file which contains details on each version and a summary of all commits in conjunction with the README.md file for each branch. 

Note that the Master branch contains the final troubleshooting directory of the EOG circuit which combines each part of element of the EOG into a final circuit. This is one of the more pivotal directories, since it combined all the elements and troubleshooted issues through testing the sine wave test signal, clean & noisy EOG, and finally the live EOG signal. It essentially features the troubleshooting that resulted in the EOG circuit detecting horizontal eye movement well. 


Final EOG Design
----------------

The final EOG design which includes images of the complete EOG circuit, videos of the EOG circuit and the electrode connections to measure a live EOG signal can be found in this **Master** Branch.

The electrodes are connected to myself and the breadboard of my EOG circuit. 

The final EOG circuit as can be seen in images **Final_EOG_Circuit1_Notch.jpg**, **Final_EOG_Circuit2_Notch.jpg** & **Final_EOG_Circuit3_Notch.jpg** (found in the **Final Circuit** directory in this Master Branch) features four small breadboards attached side-by-side with a larger breadboard towards the top. The first breadboard (furthest to the left in the image) contains two first order High Pass Active Filters which are are powered by a LM324N op amp. They originally filtered the EOG signal coming in from the 2 electrodes and attenuate the DC offset from the signal. However, after troubleshooting, it was found that this somehow attenuated the EOG signal. Thus the EOG signal coming in from the 2 electrodes is first passed through to the Instrumentation Amplifier. 

The 2 electrodes are connected to the Instrumentation Amplifier (on the second breadboard) where the signal is amplified with a gain of 100 (originally was a gain of 50, but changed when testing the live EOG signal). Once the signal has been amplified, the output is connected to a first order High Pass Active Filter (on the first breadboard) where the DC offset is attenuated. 

This output is then connected to a first order Low Pass Active Filter (on the third breadboard) with a 40 Hz cutoff frequency which attenuates the high frequency noise from the signal, including the 50 Hz powerline frequency noise. This Low Pass Active Filter is powered by a LM324N op-amp. The signal is then passed through a notch filter which attenuates the 50 Hz powerline frequency noise from the signal as this noise was causing too much noise even after the signal was low-pass filtered. The notch filter can be found on the larger, top most breadboard. 

The output after the signal has been filtered by both the low-pass filter and the notch filter is then input into both a Positive Peak Detector and a Negative Peak detector (also on the third breadboard). These two peak detectors which feature a LM324N op-amp and diodes are utilized to detect the positive and negative peaks in an EOG signal. Positive and negative comparators (featuring a LM339) are utilized in outputting a binary number (0 or 1) which corresponds to whether or not a peak is detected - with 0 meaning no peak is detected and 1 meaning a peak is detected. The output then results in an LED switching on (for an output of 1) or an LED switching off (for an output of 0). When there are positive peaks detected, a green/red LED is switched on. When there are negative peaks detected, a blue LED is switched on.

Proof of a working device can be found in the videos **Proof_of_Working_EOG_1.mp4**, **Proof_of_Working_EOG_2.mp4**, **Proof_of_Working_EOG_3.mp4**, & **Proof_of_Working_EOG_4.mp4** in the Master branch under the **Proof of Working Device** directory. Additionally, the Scope Output of the peak detector (in blue) for incoming EOG signal (yellow) can be found in images **FinalCircuit_Live_EOG_Signal_ScopeOutput1.png** & **FinalCircuit_Live_EOG_Signal_ScopeOutput2.png**. The final EOG design works well in detecting horizontal eye movement, such as when looking left (output is blue LED switched on) or right (red/green LED is switched on) or center (both LEDs are off).

Issues & Further Areas for Improvement of the Final EOG Design
--------------------------------------------------------------

The final EOG design works well in detecting eye movement, such as when looking left (output is blue LED switched on) or right (red/green LED is switched on) or center (both LEDs are off). However, there are still areas of improvement in the final EOG design. This includes:
- Creating a neater circuit, eliminating the unused parts of it. This includes the second first order high pass active filter which was originally utilized to high-pass filter the EOG signal from one of the electrodes BEFORE the instrumentation amplifier.
- Creating a smaller, attached breadboard circuit for the Notch filter instead of having it on the larger breadboard which is unattached from the other breadboards.
- Altering the circuit so that there is a gain of 50 through the instrumentation amplifier instead of the gain of 100 which is currently being utilized in the circuit.
- Further improvements to the circuit could also include adding on additional LEDs and circuitry to detect vertical eyemovement or blinking. This is a nice-to-have, but would be a great improvement to the circuit.
