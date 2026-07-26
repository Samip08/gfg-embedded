* allocates cores to the running nodes, if it runs out of cores to keep the nodes running juggles between nodes, if a publisher/subscriber in a not running node(not in the 8 cores) needs a routine action like a pub or a sub the CFS(completely fair scheduler) saves register state and runs another node on the same core
* the publisher drops its data without any acknowledgement into the DDS(data distribution service )running in the os in the background(the void), the DDS constantly monitors the traffic and instantly creates a copy and pushes it in the local buffer of the subscriber pushing a software callback function to collect

[[colcon and ament(love)]]
[[serialization and dds]]
[[blitz.py, packer.py, parser.py]]

blitz_ros
	* blitz
		* blitz 
			* pycache folder
			* [[blitz.py]]
			* [[parser.py]]
			* [[packer.py]]
			* [[interfaces.py]]
		* nodes
		* launch
			* blitz.launch.py
		* [[cmakelist.txt]]
		* [[package.xml]]
	* robot interfaces
		* .msg
		* [[cmakelist.txt]]
		* [[package.xml]]

* the struct is serialized into a flattened data stream input to the DDS, if you want yu can tune TCP to ensure guaranteed delivery or UDP blaster like a 4k video where its ultra high speed streaming of bytes and if any package is missed you dont go back to get it just leave it
* the executor then deserializes these bits to make sure its in the normal struct/class form in the local buffer for the subscriber callback
* but if you are running multiple nodes, it might directly store it in a common shared ram block to prevent routing delays or either it shares a pointer from the publisher buffer, to the subscriber buffer to ensure instantaneous relay