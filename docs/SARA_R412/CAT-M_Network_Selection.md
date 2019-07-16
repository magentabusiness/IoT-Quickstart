# Connect SARA R412 to Magenta LTE-M Network

!> Prerequisites
 >If you using R412 EVK (Evaluation kit), download m-center software from [U-Blox website download section.](https://www.u-blox.com/en/evk-downloads)  
 >Insert the Simcard in proper simcard slot and connect the antennas.  
 >If you using module, open the respective port for the AT commands.  
 >IF you using EVK, open m-center AT terminal.  

# General AT commands and response from Module
* For EVK users, just click on Get info button. Do not need to enter general information commands manually.
* For Module users, follow these AT commands.
```
AT                                  //check the module 
--> OK

ATI                                 //Module information
--> Manufacturer: u-blox
--> Model: SARA-R412M-02B
--> Revision: M0.09.00 [Jan 31 2019 18:59:31]
--> SVN: 05
--> IMEI: 35***********70
--> OK

AT+CGMI                             //Module manufacturer identification
--> u-blox
--> OK

AT+CGMM                             //Module identification
--> SARA-R412M-02B
--> OK

AT+CGMR                             //Firmware version identification
--> M0.09.00 [Jan 31 2019 18:59:31]
--> OK

AT+CCLK?                            //Clock
--> +CCLK: "80/01/06,02:08:09+00"
--> OK

AT+CGSN                             //IMEI identification
--> 35**********70
--> OK

AT+CSQ                              //Signal quality
--> +CSQ: 31,99
--> OK

```

# AT commands to connect with network and response from Module
```
AT+CMEE=2            //Report mobile termination error, 2 means error code enabled and verbose value used 
--> OK

AT+CREG=1            //Network registration status, 1 means network registration URC +CREG: <stat> enabled
--> OK

AT+CGREG=1          //GPRS network registration status, 1 means Network registration URC enabled
--> OK

AT+CEREG=1          //EPS network registration status, 1 means network registration URC +CEREG: <stat> enabled
--> OK

AT+CMGF=1          //Preferred message format, 1 means text format
--> OK

AT+CGDCONT=1,"IP","catm","0.0.0.0",0,0  // Set the APN as a "catm" for the Magenta LTE-M sim cards
--> OK

AT+URAT=7           //Radio Access Technology selection, 7 means LTE CAT-M1
--> OK

AT+COPS=?           //Check the available LTE-M network
--> +COPS: (0,"T-Mobile A","T-Mobile","23203",7),,(0,1,2,3,4),(0,1,2)
--> OK

AT+CSCON=1          //Module connected mode or Ideal mode
--> OK

AT+COPS=0           //Automatic network selection 
--> OK
--> +CREG: 2        // not registered but MT is trying to searching for the operator to register
--> +CGREG: 2
--> +CEREG: 2
--> +CSCON: 1       // Connected mode
--> +CREG: 1        // successfully registered to home network
--> +CGREG: 1
--> +CEREG: 1

AT+UCGED=5          //Channel and network environment description, 5 means RSRP and RSRQ reporting enabled
--> OK

AT+UCGED?           //RSRP and RSRQ report
--> +RSRP: 175,6400,"-053.70",
--> +RSRQ: 175,6400,"-03.20",

```

## Check IP Address
``` 
AT+CGPADDR = 1      //Show address of the PDP context 1
        Response:
        +CGPADDR: 1,10.184.84.84
        OK
```



