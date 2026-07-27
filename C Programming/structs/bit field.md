* if you wanna limit a datatype to a particular length, to save data 
struct trial{
	 int x: width of data_bits;(it is signed so assume 1 bit for sign)
}
* so if the data_bit width is 5, it cannot take +31
* When devices transmit status or information encoded into multiple bits for this type of situation bit-field is most efficient.
- Encryption routines need to access the bits within a byte in that situation bit-field is quite useful.
- or you can mention explicity unsigned int
  struct trial{
	 int x:width of data bits;(use accurate width based on 2^n)
}

* interestingly bit field is mainly for bit stripping, bit fields ensure cramming of data into given data widths, however they try to pack in a single data chunk
  unsigned int x:10;
  unsigned int y:10;
  unsigned int z:10; all fits into one int bit causing output somthing like aabbcc, not valid
* prefer using bit fields, following by 
  unsigned int x:10;
  unsigned int :0; //this makes the rest of the chunk 0, ensuring variables aren't crammed
* HOW IS THIS BETTER THAN SIMPLE DEFINITION, this ensures values dont go over 10 bits, if it goes values from int to short unsigned int and overflow remark, value got clipped.

* you cannot have pointers to bit field members, &t.x as they might not have, a byte addressable memory location
* array of bit fields are not allowed unsigned int x[10] : 5; invalid type compilation error

[checkout the questions](https://www.geeksforgeeks.org/c/bit-fields-c/)