## 1. blitz.py

#### `pack(self, msg)` -> Converts ROS to Raw Bytes

- **Data IN:** A fully populated ROS 2 Message Object

- iterates through `self.fields` and uses `getattr(msg, field)` and dynamically builds a struct format string: `"<BB" + self.struct` (Little-Endian, 2 Unsigned Chars for Header/ID, plus the payload). and forces the data through `struct.pack(fmt, 0xAA, self.id, *values)`.

- **Data OUT:** A contiguous, flat `bytes` object (`b'\xAA\x04\x00\x00\xa0\x40...'`)     

### `unpack(self, data)` -> Converts Raw Bytes to ROS

- **Data IN:** A sliced payload bytes object , the header and ID are already removed before this is called.

- Uses struct.unpack to convert the raw bytes back into a native Python tuple , makes an empty ros msg and uses, `setattr(msg, field, value)` to inject tuple values into the correct fields of the ROS message.

- **Data OUT:** A fully populated `ROS 2 Message Object` ready for the DDS void.

## 2. (ROS $\rightarrow$ MCU):`packer.py`

This is a dedicated ROS 2 Node (`serial_sender`). It runs on a `SingleThreadedExecutor`.

1. The DDS void delivers a `ROS 2 Message Object` to the `sub_callback`.

2. `packer.py` intercepts this object and passes it to the engine: `packet = schema.pack(msg)`.

3. blitz.py` processes it (as described above) and returns a raw `bytes` object.

4. `packer.py` takes that `bytes` object and calls `self.ser.write(packet)`. goes out via pyserial

## 3. (MCU $\rightarrow$ ROS): `parser.py`
uses a `while True:` loop to prevent the blocking serial port from freezing the ROS event loop.

1. The `while True:` loop reads one `bytes` object of length 1: `self.ser.read(1)`. If it is not `b'\xAA'`, it drops it , if `b'\xAA'` is found, it reads the next single `bytes` object to get the `id_byte`.

2. It uses the `id_byte` to look up the expected payload size dynamically: `struct.calcsize("=" + self.schema[id_byte].struct)`.

3. It reads exactly that many bytes from the hardware buffer, isolating the payload into a chunked `bytes` object.

4. It passes this chunked payload to the engine: `msg = schema.unpack(data)`.

5. `blitz.py` processes the bytes (as described above) and returns a fully formed `ROS 2 Message Object`.

6. `parser.py` takes the `ROS 2 Message Object` and calls `pub.publish(msg)`, blasting it into the DDS void.