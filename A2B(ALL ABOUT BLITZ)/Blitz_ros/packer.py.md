try:
            self.ser = serial.Serial(port, baud, timeout=1)
            self.get_logger().info(f"Opened serial port {port}")
        except serial.SerialException as e:
            self.get_logger().error(f"Serial error: {e}")
            self.ser = None
* tries to access available serial port="/dev/ttyACM0" at a baud rate of 115200, if not found logs error doesnt kill entire system


for name, schema in blitz_interfaces.items():
            if not schema.from_mcu:
                self.create_subscription(
                    schema.ros_msg,
                    schema.topic,
                    self.sub_callback(schema),
                    10
                )
                self.get_logger().info(f"Subscribed to {schema.topic}")

* blitz interface is split into the name and the schema/object itself if the schema has a from_mcu  true , packer does not operate on it, otherwise it has to subscribe data from dds, joy nodes... to send to mc
* for every interface it defines a particular schema, here its the custom msg type in which the value has to be packed, as a ros subscriber is stubborn and only allows one attribute as msg, this needs to be done to ensure yk how to pack the data

def sub_callback(self, schema : Blitz):
        def callback(msg):
            if not self.ser:
                return
            packet = schema.pack(msg)
            self.ser.write(packet)
            self.get_logger().info(f"Writing to Serial {msg}")
        return callback
        
* the callback function itself still has only one parameter .msg as ros needs, the serializer then makes packet = packed schema according to the custom msg type
* the serialized package is written