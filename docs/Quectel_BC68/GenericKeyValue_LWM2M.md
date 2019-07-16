# Generic String and Integer Key/Value Device Model

***DeviceType***:  tmaKeyValue  
***Model:*** V01  
***ManufacturerId:*** TMAKeyValue   
***ManufacturerName:*** TMAKeyValue  
***Protocol:*** CoAP / LWM2M 

## Device-Model

### ServiceName: StringData

```
Attributes
    StringKey  (length 20)
    StringValue (length 200)
Commands
    Request
        StringParamKey (length 20)
        StringParamValue (length 200)
    Response
        StringResponse (length 200)
```		
### ServiceName: IntData
```
Attributes
    IntKey (string/length 20)
    IntValue (int)
Commands
    Request
        IntParamKey (string/length 20)
        IntParamValue (int)
    Response
        IntResponse (int)
```	       

## CIG Plugin


### Data Reports  (Device to IoT-Gateway)
#### StringData  
Message ID: 00 with Response or 07 without Response
``` 
00<KEY_LEN><KEY><VALUE_LEN><STRING_VALUE> 
```   
***Response:***  (only with Message ID 00)   
``` 
AA00
```

#### IntData
Message ID: 01 with Response or 06 without Response
```
01<KEY_LEN><KEY><INT_VALUE>`
```
***Response***  (only with Message ID 01)
```
AA01
```

### Commands  (IoT-Gateway to Device)
***Command: StringCmd***  
***Message ID 02*** Request:  
```
02<KEY_LEN><KEY><VALUE_LEN><STRING_VALUE><MID>
```
***Message ID 04*** Response:  
```
04<ERRCODE><MID><STRING_RESPONSE>
```

***Command IntCmd***  
***Message ID 03*** Request
```
03<KEY_LEN><KEY><INT_VALUE><MID>
```
***Message ID 05*** Response
```
05<ERRCODE><MID><INT_RESPONSE>
```
        


## Parameter
|Name               |Type   |Len [Byte]   |Description   
|-------------------|-------|-------------|-----------
|KEY_LEN            |int8u  |1            |
|KEY                |String |0…200	      |   
|VALUE_LEN          |Int8u  |1	          |
|STRING_VALUE       |String |0…200	      |
|INT_VALUE          |Int16s	|2	          |
|ERRCODE            |Int8u	|1 	          |00 Success, 01 Error
|MID                |Int16u	|2	          |Command Identifier for Request/Response
|STRING_RESPONSE	|String	|0..200       |	
|INT_RESPONSE       |Int16s	|2            |


## Examples 
ASCII to Hex Converter: https://www.binaryhexconverter.com/ascii-text-to-hex-converter

## Send Data  (Device to IoT-Gateway)

### Send String Message

Key=City  (Hex: 43697479 / 4 Byte)  
Value=Wattens   (Hex: 57617474656e73 / 7 Byte)

|Commando           |Len    |Message ID   |Key_len   |Key            |value_len    |value        
|-------------------|-------|-------------|----------|---------------|-------------|-------------
|AT+QLWULDATAEX=      |14,    |00           |04        |43697479       |07           |57617474656e73  

```
AT+QLWULDATAEX=14,0004436974790757617474656e73,0x0000
```

### Send JSON String

Key=SensorData   
Value={"Temp":22.3,"Hum":20,"Weight":23}

|Commando           |len    |Message ID   |Key_len   |Key                        |value_len    |value        
|-------------------|-------|-------------|----------|---------------------------|-------------|-------------
|AT+QLWULDATAEX=      |47,    |00           |0A        |53656e736f7244617461       |33           |3a32322e332c2248756d223a32302c22576569676874223a32337d  


```
AT+QLWULDATAEX=47,000A53656e736f7244617461227b2254656d70223a32322e332c2248756d223a32302c22576569676874223a32337d,0x0000
```


## Send IntData

Key=Temp  (hex: 010454656d7 / 4 Byte)  
Value=223    

|Commando           |len    |Message ID   |Key_len   |Key                        |value        
|-------------------|-------|-------------|----------|---------------------------|-------------|-------------
|AT+QLWULDATAEX=      |08,    |01           |04        |010454656d7                |00DF 

```
AT+QLWULDATAEX=8,010454656d7000DF,0x0000
```


