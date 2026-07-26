* 32 bit microcontroller architecture
* ARM uses a non multiplexed unified memory bus layout , to maximize pipelining efficiency as incase of multiplexed input you cannot have the address and data at the same time rather it has drive ALE high recieve address then with ALE driven low collect data

* AMBA protocols(APB, AHB,AXI) have specific channels for requests:
1. APB has seperate paddr, pwdata and prdata
2. AXI has 5 seperate channels waddr, wdata, raddr, rdata, response(B)

[[Byte Lanes &  Banked Registers]]
[[Vonn Newman Architecture]]

* Fetch Decode Execute pipelining
* works technically the same as riscv in terms of exec mem and wb but all happens in multiple cycles in the execute stage.
* for a simple register writeback even riscv does it in the end of the exec stage itself, but for a complex instruction like load, ARM needs to run exec stage 3 times, once to calculate the address, once to latch onto the memory bus, third to retrieve and store into the reg


* ARM follows a load/store architecture meaning only load/store operations are allowed on memory values, all ALU operations can only be done on cpu general registers, this makes sure all ALU operations are 1 clk cycle
[[Thumb Architecture]]
[[Interrupts]]


![[Pasted image 20260714181628.png]]