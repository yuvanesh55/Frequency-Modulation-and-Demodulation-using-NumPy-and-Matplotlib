# Frequency-Modulation-and-Demodulation-using-NumPy-and-Matplotlib
### AIM
    To implement and analyze frequency modulation (FM) using Python's NumPy and Matplotlib libraries.   
### APPARATUS REQUIRED
1.	Software: Python with NumPy and Matplotlib libraries  
2.	Hardware: Personal Computer  
### THEORY 
Frequency Modulation (FM) is a method of transmitting information over a carrier wave by varying its frequency in accordance with the amplitude of the input signal (message signal). The frequency of the carrier wave is varied according to the instantaneous amplitude of the message signal. The general form of an FM signal is:


<img width="508" height="200" alt="image" src="https://github.com/user-attachments/assets/d69f6e8c-de84-4ee7-886b-0dc349407e29" />


### ALGORITHM

1.	Initialize Parameters: Set the values for carrier frequency, message frequency, sampling frequency, and frequency deviation.    
2.	Generate Time Axis: Create a time vector for the signal duration.  
3.	Generate Message Signal: Define the message signal as a cosine wave.  
4.	Compute the Integral of the Message Signal: Calculate the integral of the message signal over time.  
5.	Generate FM Signal: Apply the FM modulation formula to obtain the modulated signal.  
6.	Plot the Signals: Use Matplotlib to plot the message signal, carrier signal, and modulated signal.

### PROGRAM
```
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy.signal import hilbert
    
    Am = 8.8
    fm = 863
    fs = 863000
    Ac = 17.6
    fc = 8630
    b = 5
    
    t = np.arange(0, 2/fm, 1/fs)
    
    m = Am * np.cos(2 * np.pi * fm * t)
    c = Ac * np.cos(2 * np.pi * fc * t)
    s = Ac * np.cos(2 * np.pi * fc * t + b * np.sin(2 * np.pi * fm * t))
    
    
    ds = np.diff(s)
    analytic_signal = hilbert(ds) 
    envelope = np.abs(analytic_signal) 
    demod = envelope - np.mean(envelope)  
    demod = demod / np.max(np.abs(demod)) * Am 
    
    plt.figure(figsize=(10,8))
    
    plt.subplot(4,1,1)
    plt.plot(t, m)
    plt.title("Message Signal")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    
    plt.subplot(4,1,2)
    plt.plot(t, c)
    plt.title("Carrier Signal")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    
    plt.subplot(4,1,3)
    plt.plot(t, s)
    plt.title("Frequency Modulated Signal (FM)")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    
    plt.subplot(4,1,4)
    plt.plot(t[:-1], demod)  # ds shortens length by 1
    plt.title("Demodulated Signal (Recovered Message)")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    
    plt.tight_layout()
    plt.show()
```


### TABULATION
<img width="493" height="508" alt="image" src="https://github.com/user-attachments/assets/0a9559ba-7321-4c0d-ad0f-8891d30534b8" />

### OUTPUT
<img width="405" height="292" alt="image" src="https://github.com/user-attachments/assets/b6ed8447-7cc5-4965-a123-4729cda9a760" />

   
### RESULT
The message signal, carrier signal, and frequency modulated (FM) signal will be displayed in separate plots. The modulated signal will show frequency variations corresponding to the amplitude of the message signal.

