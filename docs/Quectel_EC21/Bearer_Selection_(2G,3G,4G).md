Bearer Selection
===================

Connect to 2G Network
--------------------------------
```javascript
AT
AT+CFUN=1
AT+QCFG="nwscanseq",1,1
AT+QCFG="nwscanmode",1
AT+CGDCONT=1,"IPV4V6","APN-name"
```
### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response   0...2G Network
+COPS: (1,"T-Mobile A","TMA","23203",0),,(0,1,2,3,4),(0,1,2)
``` 
### Connect to Network (2G)
```javascript
AT+COPS=1,2,"23203",0
//Response OK
```
### Check Connection 
```javascript 
AT+QNWINFO
//Response
+QNWINFO: "EDGE","23203","GSM 900",1

AT+QCSQ
// Response
+QCSQ: "GSM",125

AT+QPING=1,"10.112.28.10"    (If APN is private)
AT+QPING=1,"8.8.8.8"         (If APN is Public)

```

Connect to 3G Network
--------------------------------
```javascript
AT
AT+CFUN=1
AT+QCFG="nwscanseq",2,1
AT+QCFG="nwscanmode",3
AT+CGDCONT=1,"IPV4V6","APN-name"
```
### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response   2...3G Network
+COPS: (1,"T-Mobile A","TMA","23203",2),,(0,1,2,3,4),(0,1,2)
```
### Connect to Network (3G)
```javascript
AT+COPS=1,2,"23203",2
//Response OK
```
### Check Connection 
```javascript 
AT+QNWINFO
//Response
+QNWINFO: "HSPA+","23203","WCDMA 2100",10836

AT+QCSQ
// Response
+QCSQ: "WCDMA",61,-61,-6

AT+QPING=1,"10.112.28.10"    (If APN is private)
AT+QPING=1,"8.8.8.8"         (If APN is Public)

```

Connect to 4G Network
--------------------------------
```javascript
AT
AT+CFUN=1
AT+QCFG="nwscanseq",1,1
AT+QCFG="nwscanmode",4
AT+CGDCONT=1,"IPV4V6","APN-name"
```
### Check available Networks
```javascript 
AT+COPS=?  // (This command can take up to 180 sec)

//Response   7...LTE Network
+COPS: (1,"T-Mobile A","TMA","23203",7),,(0,1,2,3,4),(0,1,2)
```
### Connect to Network (LTE)
```javascript
AT+COPS=1,2,"23203",7
//Response OK
```
### Check Connection 
```javascript 
AT+QNWINFO
//Response
+QNWINFO: "FDD LTE","23203","LTE BAND 3",1300

AT+QCSQ
// Response
+QCSQ: "LTE",51,-86,118,-11

AT+QPING=1,"10.112.28.10"    (If APN is private)
AT+QPING=1,"8.8.8.8"         (If APN is Public)

```

Check IP address
--------------------------

```javascript
AT+CGPADDR
// Response
+CGPADDR: 1,"xyz.****.****.****"

```






