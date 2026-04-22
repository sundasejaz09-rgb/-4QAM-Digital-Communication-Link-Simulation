function interleaved = interleaver(coded_bits, depth)

num_bits = length(coded_bits);

cols = num_bits / depth;

matrix = reshape(coded_bits, depth, cols);

interleaved = matrix';

interleaved = interleaved(:);

end
