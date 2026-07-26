* Openmp first detects the number of cores and provides multithreading framework it splits the incoming data itself into smaller parts like splitting 1gb data into 256 mb each for 4 cores, this is then processed by AVX2 individually inside
* source data from sensors sits in a uint_32(32 bits) register however it might have smaller values , AXV2 registers have size 256 bits, so there are 8 trips to fill the YMM register
* values are not loaded using simd as it would take multiple cycles rather we use a `_mm256_loadu_si256`(this is the simd vector load) to load the data simulataneously into the 256 bit register
* the values is horizontally ORred to find the largest bit_width and it is crammed in the YMM register by shifting and ORing, this is then written to the compressed output buffer with a pointer to how many bytes have been written 
* Openmp handles coarse_grained_paralellism assigning of these chunks of data to the cores, while AVX2 handles the fine_grained_paralellism where it handles the functions on a single core data

* each core whift shift packing writes a header along the sensor data telling the type of bit packing, ex core0 might write 8.. <sensor data>, core1 might write 10... <sensor data> so the output buffer reads the header first and aligns its shift registers to unpack data perfectly without misalignment
  * threads do not wait for one to finish writing to start writing rather they estimate the memory address of first to finish then start writing from there on
  * professionally they use thread packing buffers all the cores load into that and then they all send a pointer to the final buffer mentioning their end position based on that the data is compiled back


[[Gemini Questions 1]]
