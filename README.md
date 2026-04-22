function [rx_symbols, h] = rayleigh_channel(tx_symbols, SNR_dB)

h = sqrt(0.5) * (randn(size(tx_symbols)) + 1j*randn(size(tx_symbols)));

faded_symbols = h .* tx_symbols;

rx_symbols = awgn_channel(faded_symbols, SNR_dB);

end
