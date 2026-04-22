**1. Introduction**

A digital communication system sends data (0s and 1s) from a transmitter to a receiver.
During transmission, signals are affected by noise and fading, which create errors.

To reduce errors, we use:

4QAM modulation
Convolutional coding
Interleaving

**1. Received Signal Model**

The received signal is:

**3. Rayleigh Fading**
   
Signal strength changes randomly

**5. Zero-Forcing Equalizer**

Removes channel distortion

**5. 4QAM Mapping**

Each symbol carries 2 bits

**3. System Working**

Transmitter
Generate bits
Apply encoding
Interleave bits
Map to 4QAM symbols
Channel
Adds noise and fading
Receiver
Equalize signal
Demodulate
Deinterleave
Decode

4. Flowchart
   
        TRANSMITTER
   ----------------------
   Random Bits
        ↓
   Convolutional Encoder
        ↓
     Interleaver
        ↓
     4QAM Mapper
        ↓
   ----------------------
          CHANNEL
   ----------------------
     r = h·s + n
        ↓
   ----------------------
        RECEIVER
   ----------------------
     Equalizer (r/h)
        ↓
    Demodulator
        ↓
   Deinterleaver
        ↓
   Viterbi Decoder
        ↓
     Output Bits
   
**6. Result Plot Understanding**

**1. BER vs Eb/No Plot**

X-axis → Eb/No (Signal to Noise Ratio)
Y-axis → BER (Error Rate)
Understanding:
As Eb/No increases → noise decreases → BER decreases
Coded system curve is lower than uncoded → better performance
Gap between curves = coding gain

**2. Constellation Plot**

Shows received symbols in complex plane
Understanding:
Ideal points = 4 fixed positions
Noise spreads points around them
Tight clusters → good performance
Scattered points → more errors

**7. Key Results **

Coding reduces errors significantly
Interleaving helps in fading conditions
System works well even at moderate SNR
