function coded_bits = encoder(bits)

trellis = poly2trellis(3, [5 7]);

coded_bits = convenc(bits, trellis);

end
