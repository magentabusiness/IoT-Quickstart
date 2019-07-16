
```
AT+QMTDISC=2

AT+QMTOPEN=2,"160.44.204.79",8883
AT+QMTCONN=2,"7068026a-19fe-4555-8678-48a483fcd985_0_0_2018121011","7068026a-19fe-4555-8678-48a483fcd985","868f8f6aebb971d13216484154eafbdd7c6af071843c427abb720e460aa1ac53a"

AT+QMTPUB=2,0,0,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/data/json"
AT+QMTPUB=2,0,0,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/data/json"
> {
  "identifier": "123",
  "msgType": "deviceReq",
  "hasMore": 0,
  "data": [
    {
      "serviceId": "IntData",
      "serviceData": {
        "IntKey": "MQTTVAL2",
        "IntValue": 348
      }
    }
  ]
}
} ] } } "IntValue": 34TVAL2",
^Z

OK

+QMTPUB: 2,0,0
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/json",0
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/json",0
OK

+QMTSUB: 2,1,0,0
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary",0
AT+QMTSUB=2,1,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary",0
OK

+QMTSUB: 2,1,0,0

+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","

+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","

+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","

+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","
AT
AT
OK
AT
AT
OK

+QMTRECV: 2,0,"/huawei/v1/devices/7068026a-19fe-4555-8678-48a483fcd985/command/binary","
```

