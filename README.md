function constellation(rx_symbols, SNR_dB)

gray_map = [1+1j, -1+1j, -1-1j, 1-1j] / sqrt(2);

figure('Name', 'Received Constellation');

plot(real(rx_symbols), imag(rx_symbols), 'b.', 'MarkerSize', 4);

hold on;

plot(real(gray_map), imag(gray_map), 'ro', 'MarkerSize', 10, 'LineWidth', 2);

grid on; axis equal;

xlabel('In-Phase (I)');

ylabel('Quadrature (Q)');

title(sprintf('Received 4QAM Symbols (Eb/No = %d dB)', SNR_dB));

legend('Received', 'Ideal');

xlim([-2 2]); ylim([-2 2]);

end
