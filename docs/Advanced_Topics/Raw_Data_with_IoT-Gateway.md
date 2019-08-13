# Send a Raw Data and Command to the IoT-Gateway
Before following this document, make sure you have registered your device with product model called `"Raw_Data_with_command"` in IoT-Gateway. 

[The product model `"Raw_Data_with_command"`  can be found in Product Profile Section]

## Step:1 Register device successfully with Demo product model (Raw_Data_with_Command)

## Step:2 Open putty and send data 

1. We will send the data in format of string.
   
2. Convert the String to HEX format.

3. Send the data from the Putty to IoT-Gateway.

4. Data will be received by the IoT-Gateway in base-64 format.

## Example for sending the data.

- Assume that we want to send the data "Magenta"
- String (Magenta) -----> HEX is "4d6167656e7461"
- Putty terminal should be response with confirmation.
  
       
       AT+QLWULDATA=7,4d6167656e7461
       OK

       +NNMI:8,FFFE01134C9A0000
       
-  Check the Device in the IoT-Gateway, it should receive data in base 64 format like below. Go to device History data.
   
   ![Platform Raw data](../images/data_in_platform.png)

- Received data should be look like ``"TWFnZW50YQ=="``.

- Decode the received data via Base-64 to String converter.  
  ``Base-64 (TWFnZW50YQ==) --> String (Magenta)``


     


