### Question 7: The Memory Wall (Bandwidth Limits)

> _"Your resume claims a massive 9.4 GB/s throughput. That is dangerously close to the physical bandwidth limits of single-channel DDR4 RAM. If your AVX2 engine gets so heavily optimized that it can compress data at 20 GB/s, but your RAM can physically only write data at 15 GB/s, your CPU is going to stall completely, just twiddling its thumbs waiting for the RAM to catch up. How did you profile this code to prove whether your engine is **Compute-Bound** (limited by the CPU's math speed) or **Memory-Bound** (limited by the RAM's physical speed)? And if you are Memory-Bound, how do you fix it?"_

7. <(ts sum absolute bs question bruh) that sounds like a very valid conceern, sometimes your programs compute bound speed might just be getting limited by the Memory's phycial speed at which values can be written a valid bottleneck however , that entirely depends on the device specs on what its being written so when tried on dofferent devides accros similar number of cores its giving concurrent about 3x speedup, ot ensure we are not getting capped at the physical chip writing speed we can conclude the experiment entirely in the L1 cache/SRAM with the fastest speeds>

* running the experiment entirely in the L1 cache is how we benchmark pure compute speed called _in-cache microbenchmark_.
* however sensor streams are usually gbs long while the L1 cache on each core is usually only about 32-64kb/core so its easily exhausted, so cache testing wont work we must use ram
* we can test for compute bound or memory bound system by using a model for ROOFLINE MODEL, if it tells we are memory bound , we can mitigate by software prefetching, telling the cpu to pull in the next chunk of RAM into the cache before AVX asks for it


### Question 8: Branching Inside SIMD (The If-Statement Killer)

> _"Let's say your sensor occasionally glitches and sends a corrupted error code (like `0xFFFFFFFF`). You want your engine to completely ignore and drop these bad values instead of packing them. In standard C++, you would just use an `if (val != error)`. But you are in AVX2. An AVX register processes 8 elements simultaneously; it cannot take an `if` branch for element 2 while doing math on element 3. How do you conditionally filter out bad data inside a vector register without breaking your SIMD pipeline?"_


8.<for an error code usually we prefer values liek 255 or or 0 as 0 , usually letting a small error signal pass when passing sensor data at suhc high speeds shouldnt terribly affect performance but agauin while chekcing the bitwidth this can be figured out by orring all of them and checkng that the value doesnt give tis exact error value if it does we would probably search through and find the second biggest(real value) and use that for bit chopping>

