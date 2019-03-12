# Connect BC68 to IoT-Gateway

- [Connect BC68 to IoT-Gateway](#connect-bc68-to-iot-gateway)
- [Prerequisites](#prerequisites)
- [Configure Device](#configure-device)
- [Configure Putty](#configure-putty)
- [Check Connection](#check-connection)
- [Prepare BC68 (do it only once)](#prepare-bc68-do-it-only-once)
- [Connect BC68 to NB-IoT Network and IoT-Gateway (do it after each reboot)](#connect-bc68-to-nb-iot-network-and-iot-gateway-do-it-after-each-reboot)
- [Next Step: Send data from your Device to IoT-Gateway / Link: Send DATA](#next-step-send-data-from-your-device-to-iot-gateway--link-send-data)
- [Troubleshooting](#troubleshooting)
  - [Connect manually](#connect-manually)
  - [Check Signal](#check-signal)
  - [Check IP Address](#check-ip-address)
  - [Check IoT-Gateway](#check-iot-gateway)

# Prerequisites
* [Create your first Application](../01&#32;Create&#32;first&#32;Application.md)
* [Add your first device](../02&#32;Add&#32;first&#32;Device.md)
* Install Putty   
  https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
* Download latest Drivers  
  https://www.exar.com/product/interface/uarts/usb-uarts/xr21v1412

# Configure Device
1. Insert SIM Card
2. Mount antenna
3. Check if DIP-Switch (J302) is in position: MAIN UART TO USB
4. Connect it with USB to your PC
5. Install Drivers
6. Check in Device Manager the correct COM-Port (Ch A)  
   ![Step4](../images/BC68_Step1.png)
7. Open Putty  


# Configure Putty     

   ![Putty](../images/BC68_Putty_Step1.png)    
   1. Enter correct COM-Port
   2. Set Baud rate (Speed) to 9600
   3. Connection Type: Serial
   4. Enter "BC68" as name  
   5. Press save

   ![Putty](../images/BC68_Putty_Step2.png)    
   1. Select "Terminal"
   2. Local echo: Force On
   3. Local line editing: Force On
   4. Select "Session"  

   ![Putty](../images/BC68_Putty_Step3.png)    
   1. Press Save
   2. Double-Click to "BC68" to connect Putty to your BC68 Module  


# Check Connection  
  ![Putty](../images/BC68_Putty_Step4.png)   
  Enter `ATI` to check module

# Prepare BC68  (do it only once)  
```
    AT+NCONFIG=AUTOCONNECT,FALSE         # Disable Auto connect
    AT+NRB                               # Reboot - wait until finished (10sec)
    AT+NCDP=10.112.28.10,5683            # Set IP-Address of IoT-Gateway
    AT+NBAND=8                           # Set Band 8 for T-Mobile Austria - speeds up time to connect
    AT+NRB                               # Reboot - wait until finished (10sec)
    AT+CFUN=1                            # Enable Radio Module
    AT+CGDCONT=0,"IP","alliot.nbiot.at"  # Set APN
    AT+CPSMS=0                           # Disable Power Saving Mode
    AT+QREGSWT=1                         # Automatic registration mode (IoT-Gateway)
    AT+NCONFIG=AUTOCONNECT,TRUE          # Enable Auto connect
    AT+NRB                               # Reboot - wait until finished (10sec)
```
**NOTE: The fist time to connect can take up to 10 minutes. (until CEREG: 5)**

#  Connect BC68 to NB-IoT Network and IoT-Gateway (do it after each reboot) 
```
    AT+NPSMR=1                           # Enable Power Saving Mode Status Report
    AT+CEREG=1                           # Enable network registration unsolicited 
    result code: “+CEREG:<stat>”
    AT+NNMI=1                            # Enable New Message Indications
    AT+CSCON=1                           # Enable Signalling Connection Status
```
**Responses from Module**
```

    +CEREG:2      # Search for Network  

    +CSCON:1      # Connected Mode

    +CEREG:5      # Attached to Network

    +QLWEVTIND=0  # Registration on IoT-Gateway successful

    +QLWEVTIND=3  # Ready to send Data

    ...
    +CSCON:0      # Idle Mode

    ...

    +NPSMR:1      # Power Saving Mode active

```

**If the modem responses this 2 lines you are successfully connected to IoT-Gateway and able to send and receive data**  
+QLWEVTIND=0  # Registration on IoT-Gateway successful  
+QLWEVTIND=3  # Ready to send Data  
**Otherwise start troubleshooting**

# Next Step: Send data from your Device to IoT-Gateway  / Link: [Send DATA](04_Send_Data_BC68.md)

# Troubleshooting

## Connect manually
   ```
    AT+NCONFIG=AUTOCONNECT,FALSE
    AT+NCDP=10.112.28.10,5683            # Set IP-Address of IoT-Gateway
    AT+NRB                               # Reboot - wait until finished (10sec)
    AT+NBAND=8                           # Set Band 8 for T-Mobile Austria - speeds up time to connect
    AT+CFUN=1                            # Enable Radio Module
    AT+CGDCONT=0,"IP","alliot.nbiot.at"  # Set APN
    AT+CPSMS=0                           # Disable Power Saving Mode
    AT+QREGSWT=1                         # Automatic registration mode (IoT-Gateway)
    AT+NRB                               # Reboot - wait until finished (10sec)
    AT+CFUN=1                            # Enable Radio Module
    AT+NPSMR=1                           # Enable Power Saving Mode Status Report
    AT+CEREG=1                           # Enable network registration unsolicited 
    result code: “+CEREG:<stat>”
    AT+NNMI=1                            # Enable New Message Indications
    AT+CSCON=1                           # Enable Signalling Connection Status
    AT+COPS=1,2,"23203"                  # Forces an attempt to select and register with the
                                         # network operator (23203 is T-Mobile AT) wait for 30sec – 300sec 
   ```


## Check Signal
```
AT+NUESTATS         # Query UE Statistics

        Response:
        Signal power:-815   # Signal Power in centibels (RSRP..Reference signal received quality)
        Total power:-707    # Total power in centibels  (RSSI..Received signal strength indicator)
        TX power:120        # current Tx power level in centibels
        TX time:1263        # total Tx time since last reboot in millisecond
        RX time:1914285     # total Rx time since last reboot in millisecond
        Cell ID:7164511     # last cell ID
        ECL:1               # last CoverageExtension Level [0,1,2]
        SNR:10              # last Signal to noise ratio value
        EARFCN:3547         # last Absolute radio-frequency channel number 
        PCI:186             # last Physical ID of the cell 
        RSRQ:-139           # Reference signal received quality in centibels
        OPERATOR MODE:4     # operator mode

AT+NUESTATS=CELL    # Get neighbour cells

        Response:
        #           EARFCN,PCI,A,RSRP,RSRQ,RSSI,SNR    A...1 indicates the current serving cell
        NUESTATS:CELL,3547,186,1,-813,-134,-715,10

        NUESTATS:CELL,3547,235,0,-868,-108,-1354,200

        NUESTATS:CELL,3547,244,0,-847,-108,-1354,200

        NUESTATS:CELL,3547,338,0,-874,-108,-1354,200

        NUESTATS:CELL,3547,464,0,-880,-108,-1354,200
    
```  

In case that you need support, please attach the output of `AT+NUESTATS=ALL` to your support request.

## Check IP Address
``` 
AT+CGPADDR
        Response:
        +CGPADDR:0,10.X.Y.Z


AT+NPING=10.112.28.10   # IP of IoT-Gateway, you are not able to ping any other IP address

        Response OK:
        +NPING:10.112.28.10,61,909

        Response ERROR:
        +NPINGERR:1
```

## Check IoT-Gateway  
* [Add your first device](../02&#32;Add&#32;first&#32;Device.md)
* Check if your IMEI is correct.


