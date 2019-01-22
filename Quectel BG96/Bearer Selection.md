Bearer Selection
===================

**NOTICE:** At this time no NB-IoT/2G/CAT-M Multi-SIM Card is available.  You can choose between a NB-IoT SIM Card and a 2G/CAT-M SIM Card. (December 2018)

**NOTICE:** CAT-M is currently not available in Austria. (December 2018)


Connect to NB-IoT with BG96
--------------------------------

```javascript
AT+QCFG="nwscanseq",03,1
AT+QCFG="nwscanmode",3,1
AT+QCFG="iotopmode",1,1
AT+QICSGP=1,1,"alliot.nbiot.at","","",1  //Set APN
``` 
### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response   9...NB-IoT Network
+COPS: (1,"T-Mobile A","TMA","23203",9),,(0,1,2,3,4),(0,1,2)
```

### Connect to Network (NB-IoT)
```javascript
AT+COPS=1,2,23203,9
```

### Check Connection 
```javascript 
AT+QNWINFO
//Response
+QNWINFO: "CAT-NB1","23203","LTE BAND 8",3547

AT+QCSQ
// Response
+QCSQ: "CAT-NB1",-80,-90,82,-10

AT+QPING=1,"10.112.28.10"

```


Connect to 2G (GPRS) with BG96
--------------------------------

```javascript
AT+QCFG="nwscanseq",01,1
AT+QCFG="nwscanmode",1,1
AT+QICSGP=1,1,"business.gprsinternet","","",1  //Set APN
```

### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response  8..CAT-M Network
+COPS: (2,"T-Mobile A","T-Mobile","23203",0),(3,"A1","A1","23201",0),,(0,1,2,3,4),(0,1,2)
```

### Connect to Network (2G)
```javascript
AT+QIACT=1
```

### Check Connection 
```javascript 
AT+QNWINFO
//Response:
+QNWINFO: "EDGE","23203","GSM 900",8


AT+QCSQ
// Response:
+QCSQ: "GSM",-48

AT+QIACT?
//Response
+QIACT: 1,1,1,"yourIP"


AT+QPING=1,"8.8.8.8"
```




Connect to CAT-M  with BG96
--------------------------------

```javascript
AT+QCFG="nwscanseq",02,1
AT+QCFG="nwscanmode",3,1
AT+QCFG="iotopmode",0,1
AT+QICSGP=1,1,"business.gprsinternet","","",1  //Set APN
```

### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response  8..CAT-M Network
+COPS: (0,"T-Mobile A","TMA","23203",8),,(0,1,2,3,4),(0,1,2)
```

### Connect to Network (CAT-M)
```javascript
AT+QIACT=1
```

### Check Connection 
```javascript 
AT+QNWINFO
//Response:
+QNWINFO: "CAT-M1","23203","LTE BAND 20",6400


AT+QCSQ
// Response:
+QCSQ: "CAT-M1",-33,-53,250,-5

AT+QIACT?
//Response
+QIACT: 1,1,1,"yourIP"


AT+QPING=1,"8.8.8.8"

```

Use CAT-M and fallback to 2G  
-------------------------------
```javascript
AT+QCFG="nwscanseq",0201,1  
AT+QCFG="nwscanmode",0,1  
AT+QCFG="iotopmode",0,1  
```

Use 2G and fallback to CAT-M
------------------------------
```javascript
AT+QCFG="nwscanseq",0102,1  
AT+QCFG="nwscanmode",0,1  
AT+QCFG="iotopmode",0,1  
```

Use NB-IoT and fallback to CAT-M and 2G  (Not available now)
-----------------------------------------------------------------
```javascript
AT+QCFG="nwscanseq",030201,1  
AT+QCFG="nwscanmode",0,1  
AT+QCFG="iotopmode",2,1  
```

Further Informations:  
Quectel_BG96_Network_Searching_Scheme_Introduction_V1.2.pdf @   https://www.quectel.com/Qdownload/BG96.html