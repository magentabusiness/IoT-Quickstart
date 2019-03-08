# Send data from Device to IoT-Gateway

## Prerequisites:  
* [Create your first Application](../01&#32;Create&#32;first&#32;Application.md)
* [Add your first device](../02&#32;Add&#32;first&#32;Device.md)
* [Connect device to IoT-Gateway](03_Connect_device_to_IoT-Gateway.md)
* Open Putty and connect to your device

[Detailed Information about Upload Protocol](GenericKeyValue_CoAP.md)

In this tutorial we are using the GenericKeyValue Product Model, here we always have to upload a Key and a Value (e.g Key="Tempe", Value=23).

In Production you will have a specific Product Model for your Device, then you only will upload the Value. 

FYI: ASCII to Hex Converter: https://www.binaryhexconverter.com/ascii-text-to-hex-converter
 

## Send Integer Data

Command Syntax:
```
AT+NMGS = "8        ,06    04           54656d70       000F"       
AT+NMGS =  len(dec) ,MsgId key_len(hex) key(ascii_hex) value(hex)
```
Info:  
MsgId 06 => IntData with no Response from IoT-Gateway  
MsgId 01 => Int Data with Response from IoT-Gateway / Response = (AA01)

"Temp" in ASCII (Hex) = 54656d70  (54 65 6d 70 => T e m p)    

1. Check if device is connected to NB-IoT Network  
      
2. Send Data **without** Response from IoT-Gateway   
    `AT+NMGS=8,"060454656d70000F"`     // Data: Temp=15
3. Send Data **with** Response from IoT-Gateway   
    `AT+NMGS=8,"010454656d70000A"`   //Data Temp=10  
    Response:  
    `+NNMI: 2,"AA01"`  //Response on Application Layer  
    2 ... means 2 Byte  
    AA01 ... is the Response for MessageId 01


## Send String Data

Command Syntax:
```
AT+NMGS = "15       ,00    05           436f6c6f72     07"             4d6167656e7461   
AT+NMGS =  len(dec) ,MsgId key_len(hex) key(ascii_hex) value_len(hex) value(ascii_hex) 
```
Info:  
MsgId 07 => String Data with no Response from IoT-Gateway  
MsgId 00 => String Data with Response from IoT-Gateway / Response = (AA00)

1. Send String Data with Response from IoT-Gateway  
   In this Example we will send Key=Color / Value=Magenta     
   Color in ASCII Hex = 436f6c6f72  / Len=5  
   Magenta in ASCII Hex = 4d6167656e7461 / Len=7  
   
   `AT+NMGS=15,"0005436f6c6f72074d6167656e7461"`  
   Response:
   ```
   +NNMI:2,AA00 
   ```
   2 ... means 2 Byte  
   AA00 ... is the Response for MessageId 00



2. Send JSON Data with Response from IoT-Gateway  
   Key = "DATA",  => 44415441 / len: 4  
   Value = {"Temp":22.3,"Hum":20,"Weight":23,"Color":"Magenta"} =>  
   7b2254656d70223a32322e332c2248756d223a32302c22576569676874223a32332c22436f6c6f72223a224d6167656e7461227d  / len: 52 = 0x34

   `AT+NMGS=59,"000444415441347b2254656d70223a32322e332c2248756d223a32302c22576569676874223a32332c22436f6c6f72223a224d6167656e7461227d"`  

    Response:  
   ```
   +NNMI:2,AA00 
   ```

FYI: If you don't need a response from IoT-Gateway to save traffic and power - just use MsgId 07 instead of 00

# Watch data on IoT-Gateway

## Last Data
![Latest Data](../images/Device_Data.png)
1. Choose Application
2. Select your Device
3. Select Information Tab
4. Click "See All Properties"
   
## Historical Data
![Historical Data](../images/Historical_Data_Step.png)
1. Choose Application
2. Select your Device
3. Select Historical Data Tab
4. Select the Service 
5. Select the property
6. Select the period (Hour,Day,Week,Year)
7. Click on "Search"

## ALL Historical Data
![Historical Data](../images/Device_All_Historical_Data.png)
1. Choose Application
2. Select your Device
3. Select Historical Data Tab
4. Click on "All Historical Data"

## Next Step:
[Start to get your data out of IoT-Gateway](../Application&#32;Enablement/05_Install_and_setup_Postman.md)


