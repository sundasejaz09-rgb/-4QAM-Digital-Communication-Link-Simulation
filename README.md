function ber_plots(EbNo_dB, ber_uncoded_theory, ber_coded_sim, ber_fading_sim)

figure('Name', 'BER Performance');

semilogy(EbNo_dB, ber_uncoded_theory, 'k--', 'LineWidth', 1.5);

hold on;

semilogy(EbNo_dB, ber_coded_sim, 'bo-', 'LineWidth', 1.5, 'MarkerSize', 6);

semilogy(EbNo_dB, ber_fading_sim, 'rs-', 'LineWidth', 1.5, 'MarkerSize', 6);

grid on;

xlabel('Eb/No (dB)');

ylabel('Bit Error Rate (BER)');

title('BER Performance: 4QAM with Coding');

legend('Uncoded AWGN (Theory)', 'Coded AWGN', 'Coded Rayleigh', ...

       'Location', 'southwest');
       
ylim([1e-5 1]);

end
