ROS, DDS stream data over wi-fi but to be sent to the mcu side it needs to be flattened and converted to a raw data stream
* _ innit_ defined self fields:
  1. topic: topic its subscribing/publishing to
  2. msg_id: raw bytes are thrown into mcu, to identify which class they belong to they have a custom msg id
  3. struct_fmt: python extension for structs telling the contents of struct
  4. fields: the variable names attached to these structs
  5. ros_msg: custom named message made in ros
  6. from_mcu: bool

* pack(self, msg):
  1. `for field in self.fields:
            obj = getattr(msg, field) ` 
  gets each individual value from self.fields , these are added to an empty list called values
  2. `fmt = "<BB" + self.struct`
   allows you to add 2 integers along with your normal struct, first integer is a sync number triggers the mcu to start reading , second integer is message id 
  3. `return struct.pack(fmt, 0xAA, self.id, * values)`
    fmt only is a string telling how the struct is packed say "<BBff", in little endian first two integers followed by the actual struct values 


* unpack(self, msg):
  1. `fmt = "=" + self.struct`
     read these bytes using standard native alignment , converting custom messages back to the original datatypes
  2. `unpacked = struct.unpack(fmt, data)`
     puts data through struct.unpack using blueprint fmt, chops the values into a python tuple of thier individual types
  3. ` msg = self.ros_msg()`
     makes a blank msg of the exact type needed as per fmt
  4. `for field, value in zip(self.fields, unpacked):
            `setattr(msg, field, value)`
            goes through the field containing the names and the values and maps them back and puts into msg, msg. field[0] = value[0]
            and then returns this custom struct of msg
            