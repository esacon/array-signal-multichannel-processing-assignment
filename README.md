# Array Signal and Multi-Channel Processing

## Programming Exercise

### Description

**Experimental System: Acoustic Crow’s Nest Array**

- Volumetric Microphone Array with 16 randomly distributed elements
- Condensator Microphones, frequency range: 5 Hz-100 kHz, sample frequency: 48 kHz
- Optimized for stationary or mobile operation on an unmanned ground vehicle
- Possible Applications: speech, shots, ground-based and airborne platforms

**Flight Experiment in Wachtberg**

- Crow’s Nest Array measuring the sound emitted by an Unmanned Ground Vehicle (UAV)
in flight
- **Challenge:** Determine DOA of the sound emitted by the UAV


Consider the measurements from a flight experiment delivered from the described volumetric Crow’s Nest Array with 16 elements. Channel 9 was not in operation during the experiment and is therefore missing from the measurement. In the folder `measurements` you find the pre-processed measurements of the 15 channels. The measurements contain the recording of a drone flight over the microphone array of about 100 seconds duration. The data are band-pass filtered with cut-off frequencies from 2 kHz to 20 kHz. In addition to the pre-processed data, a file containing the raw data of the first channel is included in the data set. Additionally, in the file `elements_positions.csv` you find the positions of the elements in the array.

---

### Task 1: (10 points)

Consider the 15 preprocessed audio channels containing the UAV measurements:
* Read in the prepocessed audio data from all 15 channels. If possible, use a built-in function in your programming environment, e.g. `audioread` in MATLAB.
* Plot all 15 channels one above the other over a time-axis in one figure.


#### Task 2: (14 points)

For the first audio channel, consider the pre-processed and raw data and perform the following steps for both signals:
* Transform the signal to the frequency domain via Fast Fourier Transformation with $N = 1024$. If possible, use a built-in function in your programming environment, e.g. `fft` in MATLAB.
* Plot the spectra of the signals in dB over a frequency axis and compare both spectra.


#### Task 3: (20 points)

Examine the element geometry of the considered Crow's Nest Array. Attention: The element coordinates are given in centimeters! Assume a sound velocity of $c = 343 \frac{m}{s}$.

* Compute the array factor $AF(\mathbf{u})$ for the highest considered frequency of 20 kHz.
* Plot the results in $uv$-coordinates with $u^2 + v^2 = 1$.
* Does the smallest element spacing fulfil the requirements for unambiguous DF results? If not, is this a problem?
* Calculate the maximum frequency from which the DF for the smallest element distance becomes unambiguous. Plot the array factor for this frequency.


#### Task 4: (20 points)

Now use the pre-processed data again and consider the first second of the measurement data:
* Compute the spectrum of the signal via Fast Fourier Transformation with $N = 400$. For reasons of symmetry, use only the first half of 200 values for the following steps.
* Implement the incoherent broadband beamforming function based on the array transfer vector with $K = 200$ frequency bins:

$$
BF = \sum_{k=1}^{K} \left| \mathbf{a}^H (\mathbf{u}; \omega_k) \mathbf{Z} (\omega_k) \right|^2
$$

* Calculate the function values of the beamforming function for a grid ($\alpha \in [0, 2\pi]$, $\epsilon \in [0, \pi]$) with a step size of $2^\circ$.


#### Task 5: (12 points)

* Plot the beamforming function in $uv$-coordinates.
* Determine the maximum of the Beamforming Function and the corresponding azimuth and elevation angles in degrees: $\mathbf{\hat{u}} = \arg \max_{\mathbf{u}} \sum_{k=1}^{K} \left| \mathbf{a}^H (\mathbf{u}; \omega_k) \mathbf{Z} (\omega_k) \right|^2$. An accuracy of $2^\circ$ is sufficient.

#### Task 6: (12 points)

* Now divide the audio data in 99 windows of 1 second length. For each window perform the steps described in Task 4 and 5 in order to estimate the DOA of the impinging signal.
* Plot the maximum of the beamforming function as a track in $uv$-coordinates for the complete measurement with one estimate per second
* Transform the $uv$-results into azimuth and elevation angles and plot both as a track over time.

#### Task 7: (12 points)

* In two points in time the UAV signal is overlaid by speech and the DOA of the speech is determined. Think about how the UAV can still be located here.
* Think about how to reduce noise and amplify the UAV signal with array signal processing techniques.