# Generic String and Integer Key/Value Device Model

***DeviceType***:  tmaKeyValue
***Model:*** V01
***ManufacturerId:*** TMAKeyValue 
***ManufacturerName:*** TMAKeyValue
***Protokoll:*** CoAP

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
Attributes
	IntKey (string/length 20)
	IntValue (int)
Commands
	Request
		IntParamKey (string/length 20)
		IntParamValue (int)
	Response
		IntResponse (int)
		




CIG Plugin

Data Reports  (Device to ALLIoT)
Message ID: 00  StringData
00<KEY_LEN><KEY><VALUE_LEN><STRING_VALUE>
Response: AA00

Message ID 01: IntData
01<KEY_LEN><KEY><INT_VALUE>
Response AA01

Commands  (ALLIoT to Device)
Command StringCmd
Message ID 02 Request:
	02<KEY_LEN><KEY><VALUE_LEN><STRING_VALUE><MID>
Message ID 04 Response:
	04<ERRCODE><MID><STRING_RESPONSE>
		
Command IntCmd
Message ID 03 Request
	03<KEY_LEN><KEY><INT_VALUE><MID>
Message ID 05 Response
	05<ERRCODE><MID><INT_RESPONSE>
		


Parameter
Name	Type	Len [Byte]	Description
KEY_LEN	int8u	1	
KEY	String	…200	
VALUE_LEN	Int8u	1	
STRING_VALUE	String	…200	
INT_VALUE	Int16s	2	
ERRCODE	Int8u	1 	00 Success, 01 Error
MID	Int16u	2	Command Identifier for Request/Response
STRING_RESPONSE	String	.200	
INT_RESPONSE	Int16s	2	








Examples BC68
LwM2M
AT+QLWULDATAEX=08,010454656d70000A,0x0100,1
Check AT Commands
AT+QLWSREGIND 
AT+QLWULDATA
AT+NCDP  (AT+NCDP=160.44.206.237,5683)


COAP
IntData:
Key=Temp / Value=22.3 °C / raw 223
AT+NMGS=8,"010454656d7000DF"

StringData:
Key=SensorData 
Value={"Temp":22.3,"Hum":20,"Weight":23}
AT+NMGS=47,"000A53656e736f7244617461227b2254656d70223a32322e332c2248756d223a32302c22576569676874223a32337d"

Key=VORNAME
Value=Manuel
AT+NMGS=16,"0007564f524e414d45064d616e75656c"
