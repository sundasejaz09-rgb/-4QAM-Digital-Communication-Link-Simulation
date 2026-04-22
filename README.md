function deinterleaved = deinterleaver(interleaved_bits, depth)

num_bits = length(interleaved_bits);

cols = num_bits / depth;

matrix = reshape(interleaved_bits, cols, depth)';

deinterleaved = matrix(:);

end
