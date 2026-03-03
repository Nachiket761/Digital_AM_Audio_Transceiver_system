# Digital_AM_Audio_Transceiver_system
An Introductory project into field of RF Communication Engineering

This project consists of 4 stages:
1. Modulation of analog audio signal into digital signal using pulse density modulation (PDM)
2. Generation of carrier frequency and encoding the audio signal using ON-OFF Keying (OOK)
3. Pre-amplification of raw carrier signal
4. separation of payload from carrier and demodulate digital signal back into analog signal.

**Physics**
 - stage 1: 
Nyquist-Shannon Theorem: if the sampling frequency is greater than or equal to twice the maximum frequency of a band limited signal, the original signal can be "Exactly" recreated

 - stage 2:
Electrodynamics: Accerlating charges radiate energy through Electric and Magnetic fields. LC tank circuit with some active feedback can generate frequencies in RF range but We'll be restricted because of parasitic capacitances that breadboards have

 - stage 4:
Solid state physics: as we will see, separation of payload from carrier requires a schtokky diode

**The Circuit**
 - stage 1: As we know, to sample at regular intervals we need a clock. I'm using 555 timer to generate a square wave of frequency about 90KHz which should give us about OS(over sampling of 3) assuming that we want only input frequencies till 15kHz. we didn't go upto 20Khz because that pushes the clock frequency to 1MHz which is very close to physical limits of 555 timer and also it enters RF region. Also, We will be using standard 1-Bit delta-sigma modulator
<img width="1073" height="653" alt="image" src="https://github.com/user-attachments/assets/f2577597-b88d-48b0-974b-0c0db982b322" />
<img width="1118" height="653" alt="image" src="https://github.com/user-attachments/assets/3c746740-07ea-4747-b305-37bf8918c59b" />

- stage 2: We require an oscillator circuit to generate the carrier frequency. We will be using a Clopitt's Oscillator which consists of an active feedback from a NPN BJT. Also, we will be using a Class-C amplifier configuration in combination with a tuned LC Tank to produce a AM carrier wave(with antenna attached ofc :{) and the emitter of the BJT in this amplifier is connected to a NPN BJT which performs OOK using the digita signal produced at the last stage
<img width="1385" height="759" alt="image" src="https://github.com/user-attachments/assets/27b51bb7-effb-4f61-b490-d206fb5031d3" />

 - stage 3: Now we are on the RX side. firstly, We need a Tuned LC tank to capture the signal, then we need to amplify this signal as the transmitted power attenuates according to inverse square of distance.
<img width="867" height="679" alt="image" src="https://github.com/user-attachments/assets/a95e2173-fa48-4ab0-bbf2-c395be24883c" />

 - stage 4: here We will be demodulating the OOK signal from carrier wave to produce a digital signal and this signal is properly digitized using a pair of inverting-schmitt-triggers. with this digital signal in hand the last step is to pass it through a LPF with cutoff freuency equal to the max freq of band-limited signal i.e. 15kHz and since we have sampled the signal according to nyquist limit we would get a signal very close to our input signal(why very close? delta-sigma modulation relies on averaging and noise injected at varios different stages).
<img width="1047" height="454" alt="image" src="https://github.com/user-attachments/assets/11c95927-42cd-4636-92ab-4da716c57da1" />

Now the last step is to add a LM393 Audio Amp and a speaker to hear the Audio!!
