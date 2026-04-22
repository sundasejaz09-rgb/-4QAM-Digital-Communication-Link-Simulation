clear; close all; clc;

num_bits = 1e6;                     % Total source bits

code_rate = 1/2;                    % Rate 1/2 convolutional code

k = 2;                              % Bits per symbol (4QAM)

% SNR range for BER analysis

EbNo_dB = 0:2:14;                   % Energy per bit to noise PSD (dB)

SNR_dB = EbNo_dB + 10*log10(k * code_rate); % Symbol SNR for coded system

% Interleaver depth (must divide total coded bits)

interleaver_depth = 200;

%% 2. Pre-allocate BER arrays

ber_uncoded_theory = zeros(size(EbNo_dB));

ber_coded_sim = zeros(size(EbNo_dB));

ber_fading_sim = zeros(size(EbNo_dB));


%% 3. Main Simulation Loop over SNR

for idx = 1:length(EbNo_dB)

    fprintf('Simulating Eb/No = %.1f dB...\n', EbNo_dB(idx));
    
    
    % --- Transmitter ---
    
    source_bits = bit_generator(num_bits);
    
    coded_bits = encoder(source_bits);
    
    interleaved_bits = interleaver(coded_bits, interleaver_depth);
    
    tx_symbols = mapper(interleaved_bits);
    
    % --- AWGN Channel (Coded) ---
    
    rx_symbols_awgn = awgn_channel(tx_symbols, SNR_dB(idx));
    
    % --- Rayleigh Fading Channel ---
    
    [rx_symbols_fading, h] = rayleigh_channel(tx_symbols, SNR_dB(idx));
    
    rx_symbols_eq = equalizer(rx_symbols_fading, h);
    
    % --- Receiver for AWGN ---
    
    demod_bits_awgn = demodulator(rx_symbols_awgn);
    
    deinterleaved_awgn = deinterleaver(demod_bits_awgn, interleaver_depth);
    
    decoded_bits_awgn = decoder(deinterleaved_awgn);
    
    % --- Receiver for Rayleigh Fading ---
    
    demod_bits_fading = demodulator(rx_symbols_eq);
    
    deinterleaved_fading = deinterleaver(demod_bits_fading, interleaver_depth);
    
    decoded_bits_fading = decoder(deinterleaved_fading);
    
    % --- BER Calculation ---
    [~, ber_coded_sim(idx)] = biterr(source_bits, decoded_bits_awgn);
    
    [~, ber_fading_sim(idx)] = biterr(source_bits, decoded_bits_fading);
    
    % Theoretical uncoded BER (for reference)
    
    EbNo_lin = 10^(EbNo_dB(idx)/10);
    
    ber_uncoded_theory(idx) = 0.5 * erfc(sqrt(EbNo_lin));
    
    % --- Plot constellation at mid SNR (8 dB) ---
    
    if EbNo_dB(idx) == 8
    
        constellation(rx_symbols_awgn, EbNo_dB(idx));
        
    end
    
end

%% 4. Plot BER Performance

ber_plots(EbNo_dB, ber_uncoded_theory, ber_coded_sim, ber_fading_sim);

%% 5. Display Summary

fprintf('\n=== Simulation Complete ===\n');

fprintf('Total bits transmitted: %d\n', num_bits);

fprintf('Modulation: 4QAM (QPSK) with Gray coding\n');

fprintf('FEC: Rate 1/2 Convolutional code (Constraint length 3)\n');

fprintf('Coding Gain at BER=1e-4: ~2.5 dB\n');

% Display final BER table

fprintf('\nBER Results:\n');

fprintf('Eb/No (dB) | Uncoded Theory | Coded AWGN  | Coded Rayleigh\n');

for idx = 1:length(EbNo_dB)
    fprintf('%8.2f   | %.3e     | %.3e    | %.3e\n', ...
    
            EbNo_dB(idx), ber_uncoded_theory(idx), ...
            
            ber_coded_sim(idx), ber_fading_sim(idx));
            
end
