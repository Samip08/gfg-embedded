defines the struct_fmt, ros_ids, from_mcu etc needed for packing/unpacking by blitz

* define the interface name, to allow multiple interfaces using common message types/topics
* define the topic for publishing to/subscribing from to ensure data is in its space in the dds
* the struct fmt and the field variable names, alongside the msg that needs to be rebuilt while unpacking
* alongside if its to be packed or unpacked based on from mcu or not


* ros interfaces need to be serialized before sending as these do not contain the contiguous memory allocated structs defined by user itself rather they contain a pointer to the memory location of this struct, so this .msg needs to be read by its pointer and made into serial bytes before sending
* if not you are sending a raw memory pointer , which cannot be traced back