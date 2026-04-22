function symbols = mapper(bits)

gray_map = [1+1j, -1+1j, -1-1j, 1-1j] / sqrt(2);

num_symbols = length(bits) / 2;

bit_pairs = reshape(bits, 2, num_symbols)';

indices = 2*bit_pairs(:,1) + bit_pairs(:,2) + 1;

symbols = gray_map(indices).';

end
