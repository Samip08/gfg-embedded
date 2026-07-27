dds is basically the space under your bed where the monster lives,
* a node publishes data, it goes to its data_write buffer where they get serialized to send raw bytes, then it uses a mechanism called discovery , it sends out the ip, topic its publishing to valid data_read buffers send and invite
* the data_read of the subscriber sends its ip and then the data is sent directly to the data_read buffer where its deserialized and the subscriber callback picks it up

packeting:
serialization isnt the same as packaging as sending data over a USB wire requires you to ensure that the data is wrapped in packets before being sent 