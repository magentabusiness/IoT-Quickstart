# Connect SARA R412 to Magenta NB-IoT Network

!> Prerequisites
 > If you using R412 EVK (Evaluation kit), download m-center software from [U-Blox website download section.](https://www.u-blox.com/en/evk-downloads)  
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
--> +CSQ: 18,99
--> OK

```

# AT commands to connect with NBIoT network and response from Module
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

AT+CGDCONT=1,"IP","m2m.nbiot.t-mobile.at","0.0.0.0",0,0  // Set the APN as a "m2m.nbiot.t-mobile.at" for the Magenta NBIoT sim cards
--> OK

AT+URAT=8           //Radio Access Technology selection, 8 means LTE-NB
--> OK

AT+CSCON=1          //Module connected mode or Ideal mode
--> OK

AT+COPS=1,2,"23203",9   //Manually network selection, 23203 is PLMN code for Magenta Telekom
--> OK
--> +CSCON: 1       // Connected mode
--> +CREG: 3        // registration denied 
    .
    .
--> +CGREG: 5       // successfully registered to roaming network
--> +CEREG: 5       // successfully registered to roaming network

AT+UCGED=5          //Channel and network environment description, 5 means RSRP and RSRQ reporting enabled
--> OK

AT+UCGED?           //RSRP and RSRQ report
--> +RSRP: 030,3547,"-044.00",127,3547,"-091.90",254,3547,"-089.90",
--> +RSRQ: 030,3547,"-14.40",127,3547,"-14.70",254,3547,"-11.20",
--> OK

AT+CSQ              //Signal Quality
--> +CSQ: 18,99
--> OK

AT+CEMODE?          //Check the CE level
--> +CEMODE: 2
--> OK

```

## Check IP Address
``` 
AT+CGPADDR = 1      //Show address of the PDP context 1
        Response:
        +CGPADDR: 1,10.***.**.**
        OK
```



