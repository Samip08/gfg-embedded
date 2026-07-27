#### Question 4: The Endianness Nightmare

> _"When you use vector shifts to pack 10-bit values into a continuous bitstream, you eventually write those bytes to RAM. x86 architectures (like Intel and AMD) are strictly **Little-Endian**, meaning the least significant byte of an integer is stored at the lowest memory address. If a 10-bit value crosses a byte boundary in your output buffer, how does the CPU's Little-Endian byte ordering affect the way the bits are physically laid out in RAM? Does your algorithm have to manually reverse the bytes, or does the hardware handle it seamlessly during the unpack phase?"_


4. <the little endian is not a problem hardware handles it without any algoritm to manually reverse the bits as it just needs to pick and place imagine a number is coming as 0011 and 1111 which was originally 0011 1111 now even if it came reverse the whole stream would ocme reverse like 1111 and 0011 we just have to place i tlike 1111 goes lower byte 0011 goes hgiher byte>(B)

* If you use AVX2 vector store instructions (like `_mm256_storeu_si256`), the x86 CPU physically writes the 256-bit register to RAM using its native Little-Endian format. When your decompression engine reads it back using `_mm256_loadu_si256`, it reads it back in the exact same Little-Endian format.
* but if you use an intel chip it will write back in the reverse format and you will read garbage unless you manually swap them

#### Question 5: OpenMP Overhead & Amdahl's Law

> _"You use OpenMP to fork threads and divide the array. However, spinning up threads and synchronizing them at the end of the block has a measurable time cost (often in the microseconds). If a user passes a very small array of sensor data—say, only 2 kilobytes—the time it takes OpenMP to manage the threads will actually take longer than if a single core just compressed the data by itself. How does your engine calculate the 'threshold' to decide when to use OpenMP versus when to fall back to a purely single-threaded execution?"_

5. <usually the usacase of this project is for unloading large amounts of data as demonstrated at about 10gb/sec so the overhead due to multithreading dies out, however this is a very valid question as even in pretesting stages there was a drop in the speed due to either inefficient core usage or smaller datasets, this is usually taken care of by the input buffer dynamically if it sees a smaller user intput a normal loop unrolling happens without mutlithreading incase the overhead from that is seen larger>(A)
* There is a dynamic thresholding if statement: If the array is smaller than, say, 64KB, you bypass OpenMP entirely and just route the data straight to a single-threaded AVX2 loop. It avoids the thread-creation penalty and processes the tiny chunk instantly. 

#### Question 6: CPU Pipelining & Instruction Latency

> _"AVX2 instructions are fast, but they don't execute in 0 cycles. A vector shift instruction (`_mm256_sllv_epi32`) might have a latency of 2 or 3 clock cycles. If your C++ loop issues a shift, and the very next line of code requires the result of that shift, the CPU pipeline stalls and wastes clock cycles waiting for the hardware to finish. Did you implement **Loop Unrolling** or **Instruction Interleaving** inside the AVX2 loop to hide this instruction latency and keep the CPU execution ports fully fed?"_


6. <the loop is unrolled instead of instruction interweaving as that case there;s a lot of smaller overheads when collecting data from the final buffers which would include the out of order mess of data or even the fact that some cores might have different bitwidth so itd better to pick the whole core's data together>(F)


* absolute bs this is about loop unrolling incase instructions are 
`A= load(i)`
`B=shift(A)`
`store(B)`
loop is unrolled and instructions are interweaved to remove clk misses like

A1 = load(0x00000000)
A2 = load(0x00000004)
A3 = load(0x00000008)
B1 = shift(A1)
B2 = shift(A2)
B3 = shift(A3)
store(B1)
store(B2)
store(B3)


[[Gemini Questions 3]]