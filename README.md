function rx_symbols = awgn_channel(tx_symbols, SNR_dB)

Es = 1;

snr_linear = 10^(SNR_dB / 10);

noise_variance = Es / (2 * snr_linear);

noise = sqrt(noise_variance) * (randn(size(tx_symbols)) + 1j*randn(size(tx_symbols)));

rx_symbols = tx_symbols + noise;

end
