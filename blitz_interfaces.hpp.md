pragma pack is vital here because the esp might be checking for data without padding while the computer adds padding so we need to ensure all padding is removed

enum PacketID : uint8_t {
    VELOCITIES = 1,
};

* mapping the structs incoming to their particular msg_ids so we know how to unpack each

 #pragma pack(push, 1)
 struct velocities {
     float vx;
     float vy;
     float vz;
 };  
 #pragma pack(pop)

* since we are to memcopy the bytes of data directly instead of looking at what each mean, it is essential we have all of the data clustered to the correct size to unpack

size_t get_packet_size(uint8_t id) {
    switch (id) {
        case VELOCITY:           return sizeof(Velocity);
        default:                 return 0; // unknown
    }
}

* size is sent back to the blitz.hpp for unpacking/packing