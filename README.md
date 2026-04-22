function decoded_bits = decoder(coded_bits)

trellis = poly2trellis(3, [5 7]);

decoded_bits = vitdec(coded_bits, trellis, 5, 'trunc', 'hard');

end
