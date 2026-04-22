1. Introduction

A digital communication system sends data (0s and 1s) from a transmitter to a receiver.
During transmission, signals are affected by noise and fading, which create errors.

To reduce errors, we use:

4QAM modulation
Convolutional coding
Interleaving
2. Important Concepts with Formulas
1. Received Signal Model

The received signal is:

r=h⋅s+n

Where:

r = received signal
s = transmitted signal
h = channel effect (fading)
n = noise
2. AWGN Noise
n∼CN(0,σ
2
)
Noise is random with variance σ
2
3. Rayleigh Fading
h∼CN(0,1)
Signal strength changes randomly
4. Zero-Forcing Equalizer
s
^
=
h
r
	​

Removes channel distortion
5. 4QAM Mapping

Symbols:

2
	​

1
	​

(±1±j)
Each symbol carries 2 bits
3. System Working
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
5. Important MATLAB Code Lines
1. Bit Generation
bits = randi([0 1], 1, 1e6);
2. Convolutional Encoding
trellis = poly2trellis(3, [5 7]);
encoded_bits = convenc(bits, trellis);
3. Interleaving
interleaved = reshape(encoded_bits, [], 4).';
interleaved = interleaved(:);
4. 4QAM Mapping
symbols = (2*bits(1:2:end)-1) + 1j*(2*bits(2:2:end)-1);
symbols = symbols / sqrt(2);
5. AWGN Channel
noise = sqrt(sigma2)*(randn + 1j*randn);
r = s + noise;
6. Rayleigh Channel
h = sqrt(0.5)*(randn + 1j*randn);
r = h.*s + noise;
7. Equalization
s_hat = r ./ h;
8. Viterbi Decoding
decoded = vitdec(received_bits, trellis, 34, 'trunc', 'hard');
6. Result Plot Understanding
1. BER vs Eb/No Plot
X-axis → Eb/No (Signal to Noise Ratio)
Y-axis → BER (Error Rate)
Understanding:
As Eb/No increases → noise decreases → BER decreases
Coded system curve is lower than uncoded → better performance
Gap between curves = coding gain
2. Constellation Plot
Shows received symbols in complex plane
Understanding:
Ideal points = 4 fixed positions
Noise spreads points around them
Tight clusters → good performance
Scattered points → more errors
7. Key Results 
Coding reduces errors significantly
Interleaving helps in fading conditions
System works well even at moderate SNR
