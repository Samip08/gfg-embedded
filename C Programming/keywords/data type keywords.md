*  data type keywords: used to define the type of data they can store
 int(4 bytes, -2gb to 2g storage, %d), char(%c), float(4 bytes, %f), double(8 bytes, %lf), void(no return), short, long, signed, unsigned
 * unlike int, which is stored in memory as binary format, float/double follow IEEE standard , sign, biased exponent, mantissa(fraction)
 *  signed bit numbers have +0, -0 in normal bit system, are not cyclic(111-000), bit extension isnt same for positive, negative.(4 bit -5 is 1101 5 bit 10101, msb is sign, rest is normal number)
 * for 1's complement representation , +0/-0 case, we can utliize only n-1 bits for representation, but numbers are cyclic, sign extension easier(0 for positive, 1 for negative)
 * 2's complement ensures no ambiguity for 0 , cyclic values (+7 goes to -8)
