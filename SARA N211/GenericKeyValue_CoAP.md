# Generic String and Integer Key/Value Device Model

***DeviceType***:  tmaKeyValue  
***Model:*** V01  
***ManufacturerId:*** TMAKeyValue   
***ManufacturerName:*** TMAKeyValue  
***Protocol:*** CoAP  

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
***Message ID: 00 ***   StringData  
``` 
00<KEY_LEN><KEY><VALUE_LEN><STRING_VALUE> 
```   
***Response:***    
``` 
AA00
```

***Message ID 01*** IntData
```
01<KEY_LEN><KEY><INT_VALUE>
```
***Response*** 
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
        


### Parameter

|Name               |Type        |Len [Byte]   |Description   
|-------------------|------------|-------------|-----------
|KEY_LEN            |int8u       |1            |
|KEY                |String      |0…200	       |   
|VALUE_LEN          |Int8u       |1	           |
|STRING_VALUE       |String      |0…200	       |
|INT_VALUE          |Int16s	     |2	           |
|ERRCODE            |Int8u	     |1            |00 Success, 01 Error
|MID                |Int16u	     |2	           |Command Identifier for Request/Response
|STRING_RESPONSE	|String	     |0..200       |	
|INT_RESPONSE       |Int16s	     |2            |


## Examples 
ASCII to Hex Converter: https://www.binaryhexconverter.com/ascii-text-to-hex-converter

## Send Data  (Device to IoT-Gateway)

### Send String Message

Key=City  (Hex: 43697479 / 4 Byte)
Value=Wattens   (Hex: 57617474656e73 / 7 Byte)

|Commando           |Length |Message_ID   |Key_len   |Key            |value_len    |value        
|-------------------|-------|-------------|----------|---------------|-------------|-------------
|AT+NMGS=           |14,    |00           |04        |43697479       |07           |57617474656e73  

```
AT+NMGS=14,"0004436974790757617474656e73"
```

### Send Json String

Key=SensorData 
Value={"Temp":22.3,"Hum":20,"Weight":23}

|Commando           |Length |Message_ID   |Key_len   |Key                        |value_len    |value        
|-------------------|-------|-------------|----------|---------------------------|-------------|-------------
|AT+NMGS=           |47,    |00           |0A        |53656e736f7244617461       |33           |3a32322e332c2248756d223a32302c22576569676874223a32337d  


AT+NMGS=47,"000A53656e736f7244617461227b2254656d70223a32322e332c2248756d223a32302c22576569676874223a32337d"



## Send IntData

Key=Temp    (hex: 010454656d7 / 4 Byte)
Value=22.3 °C / raw 223  

|Commando           |Length |Message_ID   |Key_len   |Key                        |value        
|-------------------|-------|-------------|----------|---------------------------|-------------|-------------
|AT+NMGS=           |08,    |01           |04        |010454656d7                |00DF 

AT+NMGS=8,"010454656d7000DF"  




