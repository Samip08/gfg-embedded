for name, schema in blitz_interfaces.items():
            if schema.from_mcu:
                schema.pub = self.create_publisher(schema.ros_msg, schema.topic, 10)

* parser only functions when the data from mcu side needs to be put into dds/ros, so from_mcu is true , we make a publisher to publish into the dds side

 if self.ser.in_waiting >= 1:  
            header = self.ser.read(1)
            if header[0] != 0xAA:
                return  # resync
            id_byte = self.ser.read(1)[0]

*  searches for sync bit 170 only proceeds if found or else goes to continuous searching for sync byte state, then gets the msg id

try :
                    self.schema[id_byte].payload_data = self.ser.read(struct.calcsize("="+self.schema[id_byte].struct))
                    data = self.schema[id_byte].payload_data
                    if data is not None:
                        msg = self.schema[id_byte].unpack(data)
                        # self.get_logger().info(f"msg received from mcu {msg}")
                        self.schema[id_byte].pub.publish(msg)
                except KeyError:
                    self.get_logger().error(f"Received msg ID {id_byte}, ID mismatch, dropping data check configuration")

* looks up the schema blueprint and finds the type of struct needed to unpack this data , calculates the size and tells to read only that many bytes or else it might eat up into the upcoming sync byte
* then unpacks the data into the created struct based on the msg id
