Communication Settings for Ladder Program Downloading
1. FT230X Basic Uart Driver for FATEK PLC (for USB Serial Converter and USB Serial Port driver)
2. Download Program (Communication settings) :
Port Number : COM9
Station Number : 1
Baudrate : 38400
Data Bits : 7-bit
Parity : Even

Modbus RTU Communication between FATEK PLC and PC using OPC Server :
Requirements :
1. FATEK PLC FBs-20MCT2-AC
2. CB55-7 RS485 Module
3. RS485 to USB Converter
4. WinProLadder Software
5. OPC Server Software

FATEK PLC as Master and PC as Slave.
1. Hardware Settings
   - Using CB55-7 (RS485) Module
   - Using Port 2 (RS485 Channel 2) with resistor termination setting set       to "ON" position
   - Media for communication between Fatek PLC and PC is using Serial      RS485 to USB converter

2. Ladder Diagram and WinProLadder settings
   - Using FUN150 Modbus Instruction
   - PLC -> Settings -> Port 2 Parameter :
     Baudrate : 9600
     Parity : None
     Data Bit : 8 bits
     Stop Bit : 1 bit
   - Table Edit -> ModBus Master Table -> add ModBus Master Table
     add ModBus Master Table Command Item with this settings :
     (for boolean type) with Write operation to slave
     * Slave Station : 1
     * Command : Write
     * Data Size : 1
     * Master Data Start Address : M5
     * Slave Data Start Address : 000001
     That setting means writing data to the slave with ID 1 at address          000001 with the source data from master at address M5 (boolean data)
     
     Read operation from slave (boolean type)
     * slave Station : 1
     * Command : read
     * Data Size : 1
     * Master Data Start Address : M6
     * Slave Data Start Address : 000002
     That setting means master is trying to read data from slave with ID 1      at address 000002 and data that is obtained from slave is saved at         address M6 in Master data memory

     Write command for Register:
     * Slave Station : 1
     * Command : Write
     * Data Size : 20
     * Master Data Start Address : R200
     * Slave Data Start Address : 400500
     That means that Master will write data contained at address R200 to      Slave with ID 1 at address 400500

3. OPC Server Settings
   - Device Driver : Modbus Slave RTU Serial
   - Communication Serial Port Settings : same as Port 2 Parameter      Settings in PLC
   - Tag properties "address" in OPC Server must be same with address in      ModBus Master Table in WinProLadder slave address settings
