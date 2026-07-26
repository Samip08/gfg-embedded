template<typename T_pack>
std::vector<uint8_t> pack_data(T_pack data, uint8_t id) {
    size_t total_bytes = sizeof(T_pack);
    std::vector<uint8_t> buffer(total_bytes);
    std::memcpy(buffer.data(), &data, total_bytes);

    buffer.insert(buffer.begin(), id);
    return buffer;
}

* packing data to be sent over a usb wire, T_pack data tells the schema we follow so , you can approximate how many bytes of data does the buffer hold, so we can directly memcpy, it copies from the given address the given number of bits, without any idea of what dataype/struct raw binary

template<typename T_parse>
T_parse parse_struct(std::vector<uint8_t>& payload) {
    T_parse result;
    payload.erase(payload.begin());
    std::memcpy(&result, payload.data(), sizeof(T_parse));
    return result;
}

* takes everything in a temporary struct called result except the id byte, if the values have the exact mem layout as the struct everything aligns properly all float int everything

void send_data(const std::vector<uint8_t>& buffer) {
    if (Serial) {
        uint8_t header = 0xAA;  
        Serial.write(&header, 1);                 // send header first
        Serial.write(buffer.data(), buffer.size()); // send payload
    }
}

* send data function sends header bit 0xAA followed by the struct bytes

std::vector<uint8_t> receive_data() {
    static std::vector<uint8_t> buffer;

    // read all available bytes from Serial
    while (Serial.available()) {
        buffer.push_back(Serial.read());
    }

    // looping until we can return a full packet or buffer is empty
    while (buffer.size() >= 2) { // need at least header + ID
        // find the header 0xAA
        if (buffer[0] != 0xAA) {
            // header not at start, remove the first byte and continue
            buffer.erase(buffer.begin());
            continue;
        }

        // check ID
        uint8_t id = buffer[1];
        size_t expected_size = get_packet_size(id);
        if (expected_size == 0) {
            // unkown id
            buffer.erase(buffer.begin(), buffer.begin() + 1);
            continue;
        }

        // check if full data is available
        if (buffer.size() >= 2 + expected_size) {
            // slice for id + data (1 byte id + expected_size bytes data)
            std::vector<uint8_t> packet(buffer.begin() + 1, buffer.begin() + 2 + expected_size);
            // remove consumed bytes from buffer (1 byte header + 1 byte id + expected_size bytes data)
            buffer.erase(buffer.begin(), buffer.begin() + 2 + expected_size);
            return packet;
        } else {
            // wait for more bytes
            break;
        }
    }

    // No full packet yet
    return {};
}

* checks for header byte if not there erases, if id is 0 erases, if not those gets expected size from the struct, adds header and id and keeps