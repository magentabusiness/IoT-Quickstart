
# Getting Started with BG96 and MQTTS Create Device with Initial Password Mode!!
Server: 160.44.204.79  
Port: 8883  
ClientID: <<DeviceID>>_0_0_YYYYMMDDhh  
Username: <<DeviceID>>

Passwort How To:  
http://tool.oschina.net/encrypt?type=2  
Translate to EN or DE :-)
Or Better:  
https://codebeautify.org/hmac-generator

ClearText (Plain or Chiper Text): `secret`  

Algorithm: HmacSHA256  
Key: YYYYMMDDhh -- same as in the ClientID  
Hash-Value is the Password!  

Certificates (PEM Format)  




Publish Data:   
Topic: ```/huawei/v1/devices/<<DeviceID>>/data/json```

Payload:  Example for KeyValue
```
{
  "identifier": "123",
  "msgType": "deviceReq",
  "hasMore": 0,
  "data": [
    {
      "serviceId": "IntData",
      "serviceData": {
        "IntKey": "MQTTVAL2",
        "IntValue": 34
      }
    }
  ]
}

```

/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/data/json

AT+QMTPUB=?
+QMTPUB : <tcpconnectID>,<msgID>,<qos>,<retain>,“<topic>”
OK
//Publish messages.
AT+QMTPUB=2,0,0,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/data/json"
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/data/json",0

AT+QMTSUB=2,1,"#",0

