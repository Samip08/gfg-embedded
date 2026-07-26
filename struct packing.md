  struct size not same as size of all members, includes struct padding to ensure easier for cpu to access, lesser cycles needed to read
A PARTICULAR MEMBER OF A STRUCT CAN START ONLY AT A MULTIPLE OF ITS SIZE , char+short is 1+1(padding)+2 not 1+2 +padding
* but incase we wana save memory 1. #pragma pack(1),    
  2.__ attribute__((packed))
* incase it is packed without struct padding bits ,compiler reads data as chunks of 4 bytes each, incase there is no padding the struct might not occupy mem as a multiple of 4 bytes, in that case compiler does overhead bit shifting to bring both the current struct member and the forward memory location data, including standard lib
 * #pragma pack(pop) ends the clause saying only the struct bw #pragma pack(1) and #pragma pack(pop) is ensured without padding, without pop might ruin the entire code base
* IN A 32 BIT ARCHITECTURE say struct [int[0-3], char[4]], int[5-8] then first read gives the struct int member , second read needs a scrapping of bits [5,6,7] to get char, further compiler asks for read[8-11] fails to find int and has to recall [4-7] scrap [4], then call [8-11] and merge to form int
* in 64 bit architecures this chunk is 8 byte, ex 
*typedef struct structc_tag
{
    char c;
    double d;
    int s;
} structc_t; // total size here 1->8, 8, 4->8 = 24 bytes

typedef struct structd_tag
{
    double d;
    int s;
    char c;
} structd_t; // total size here 8-.8, 1,2->8(5 extra bytes) = 16 bytes, same data as above

* reduce unneccesary struct padding by:
1. placing larger data before smaller ones
2. dont mix large and small data
3. make grps w similar sizes

* 32 bit architecture has 32 lines in parallel routed to allow values directly into the general cpu registers(4 bytes),  64 bit architecture routes 64 lines in parallel , as general registers hold 64 bits(8 bytes)