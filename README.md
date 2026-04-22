function bits = demodulator(rx_symbols)

gray_map = [1+1j, -1+1j, -1-1j, 1-1j] / sqrt(2);

rx_vec = rx_symbols(:);

num_symbols = length(rx_vec);

detected_indices = zeros(num_symbols, 1);

for i = 1:num_symbols
    distances = abs(rx_vec(i) - gray_map);
    
    [~, detected_indices(i)] = min(distances);
    
end

bits = zeros(2*num_symbols, 1);

for i = 1:num_symbols

    switch detected_indices(i)
    
        case 1
        
            bits(2*i-1 : 2*i) = [0; 0];
            
        case 2
        
            bits(2*i-1 : 2*i) = [0; 1];
            
        case 3
        
            bits(2*i-1 : 2*i) = [1; 1];
            
        case 4
        
            bits(2*i-1 : 2*i) = [1; 0];
    end
end

end
