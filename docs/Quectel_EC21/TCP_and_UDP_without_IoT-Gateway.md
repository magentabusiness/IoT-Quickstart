To send the TCP and UDP data to remote server, make sure your UE connected with respective network (2G,3G,4G) and public APN. If UE is not connected with Network, kindly follow the document [Bearer selection.](./Bearer_Selection_(2G,3G,4G).md)

### Check IP address

```javascript
AT+CGPADDR
// Response
+CGPADDR: 1,"xyz.****.****.****"
```

Send/Receive data to remote server using TCP
-------------------------------------
```javascript
AT+QIOPEN=1,0,"TCP","remote TCP server IP",port,0,1 //Context is 1 and <connectID> is 0.

---> OK
---> +QIOPEN: 0,0

AT+QISTATE=1,0   //Query if the connection state of <connectID> is 0.

---> +QISTATE: 0,"TCP","IP",port,21275,2,1,0,0,"usbat"
---> OK


AT+QISEND=0,4   //Send fixed length data and the data length is 4, If random length need to be sent use AT+QISEND=0.
    > ABCD  (press Ctlr+Z, depends on your terminal Cltr+Z is for putty)
----> SEND OK

```
### Read received TCP data from remote sever
```javascript
+QIURC: "recv",0  (Notification for received data)

AT+QIRD=0
---> +QIRD: 5  (length of received data)
---> 01234     (received data)
```

Send/Receive data to remote server using UDP
--------------------------------------
```javascript
AT+QIOPEN=1,2,"UDP SERVICE","remote UDP sever IP",0,port,0  //Start a UDP service. The <connectID> is 2 and <context> is 1.
---> OK
---> +QIOPEN: 2,0

AT+QISTATE=0,1  //Query if the connection status of <contextID> is 1.
---> +QISTATE: 2,"UDP SERVICE","Server IP",0,port,2,1,2,0,"usbat"
---> OK


AT+QISEND=2,10,"Server IP",port    //Send 10 bytes data to remote
    > 0123456789  (press Ctlr+Z, depends on your terminal Cltr+Z is for putty)
----> SEND OK

```

### Read received UDP data from remote sever

```javascript
+QIURC: "recv",0  (Notification for received data)

AT+QIRD=0
---> +QIRD: 5  (length of received data)
---> 01234     (received data)

```