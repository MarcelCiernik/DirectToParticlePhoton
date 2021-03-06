# DirectToParticlePhoton

## Introdaction
DirectToParticlePhoton is an open source software for [Particle](https://docs.particle.io/faq/particle-tools/eclipse-debug/photon/). The DirectToParticlePhoton application allows to connect Particle Photon wirelessly __without necessity to use internet__ and __without need to have Particle Account__ (to be able to build and flas the device). One of the most significant advantages of this approach is the response speed. Avoiding sending the message over internet saves a lot of time.  The application is addressed for Android device, IOs Device or Microsoft mobile device. 

Its major functionality is to enable/disable all available pins (digital/analog) and allow to send/receive messages over RS232 protocol. 

<img src="https://raw.githubusercontent.com/MarcelCiernik/DirectToParticlePhoton/master/rsz_screenshot_20180205-142924.png" width="300">

## Functional Pins:

* Digital pins: D0..D7 Enable/Disable (green flashing indicates pin enabled)
* Analog pins Pin A0..A5 set a value from 0..255 
* RS232 – Send Receive message. 
* RS203 baud Rate setting.
* Device information retrieval.

<img src="https://raw.githubusercontent.com/MarcelCiernik/DirectToParticlePhoton/master/Screenshot_20180207-132939.png" width="300">



## Flas Photon with the application

There are essentially two ways how to load this application into Particle Photon.

* Load the assembly (.elf) file into the Particle photon
* Compile the software and use IDE, such as Eclipse to compile and load the software.


## Flash assembly (.elf) file directly into Photon

Put the device in DFU mode (blinking yellow) and execute: particle flash --usb target/blinkled.bin

### Compile and Build source with Eclipse IDE

Download the sources and use [these](https://docs.particle.io/faq/particle-tools/eclipse-debug/core/) instruction to build the sources with eclipse. 

### Compile and flash application via Particle Clound

In order to build the source in cloud, it is necessary to replace MANUAL flag with AUTOMATIC or SEMI_AUTOMATIC in the SYSTEM_MODE(MANUAL) macro, present in the Top of the Main.cpp file. Then follow the [link](https://docs.particle.io/guide/getting-started/modes/photon/).

## DirectToParticlePhoton http services published for Analog and Digital pins

### Connect

|Request   |Response     |
| -------- | ------------|
| "Connect" |  {"Status":"Connected/{Error}","D0..7":"'value'","A0..A7":"{Read/Write response*}","DAC":"'value'","Error":"{Description}"}

*Read/Write response defined in 'Read/Write response' Section below.


### Pins:

DirectToParticle application is http based, and all the individual functionality are triggered by a request.
The request/response list with baseUrl http:192.168.0.1 :

When the photon device is running and its pins (digital or analog) are configured to specific values, it keeps the setting as long as it is power on. This means, that if a particular set up has been made with a mobile device, and the application on the phone is turned off, the mobile application will read the current device setup on the next Connect function and adjust itself accordingly.



| Pin Name      | Get Status      | Request Enable  | Request Disable  | Response  JSON   | Error  JSON                     |
| ------------- | ----------------| ----------------|------------------|------------------|---------------------------------|
| Pin D0        | baseUrl/D0      | baseUrl/D0=true | baseUrl/D0=false | {"D0":"'value'"} | {"Error":"'Error Description'"} |
| Pin D1        | baseUrl/D1      | baseUrl/D1=true | baseUrl/D1=false | {"D1":"'value'"} | {"Error":"'Error Description'"} |
| Pin D2        | baseUrl/D2      | baseUrl/D2=true | baseUrl/D2=false | {"D2":"'value'"} | {"Error":"'Error Description'"} |
| Pin D3        | baseUrl/D3      | baseUrl/D3=true | baseUrl/D3=false | {"D3":"'value'"} | {"Error":"'Error Description'"} |
| Pin D4        | baseUrl/D4      | baseUrl/D4=true | baseUrl/D4=false | {"D4":"'value'"} | {"Error":"'Error Description'"} |
| Pin D5        | baseUrl/D5      | baseUrl/D5=true | baseUrl/D5=false | {"D5":"'value'"} | {"Error":"'Error Description'"} |
| Pin D6        | baseUrl/D6      | baseUrl/D6=true | baseUrl/D6=false | {"D6":"'value'"} | {"Error":"'Error Description'"} |
| Pin D7        | baseUrl/D7      | baseUrl/D7=true | baseUrl/D7=false | {"D7":"'value'"} | {"Error":"'Error Description'"} |

### Analog Pins:

The Particle Device contains 7 analog pins, which can be in either write or read mode. The value ranges from 0 to 4095. Each individual pin can be configured to write or read values. For more information see [datasheet](https://docs.particle.io/datasheets/photon-(wifi)/photon-datasheet/).

When request sent to write a value, the value will be constantly written to keep the pin output corresponding to the requested value.

To read a value from the analog pin, it is also necessary to set up the frequency the value will be red from the analog pin.

#### Write Mode
| Pin Name | Get Status  | Request Enable        | Request Disable |
| -------- | ------------| ----------------------|-----------------|
| Pin A0   | baseUrl/A0  | baseUrl/WA0={1..4095} | baseUrl/WA0=0   |
| Pin A1   | baseUrl/A1  | baseUrl/WA1={1..4095} | baseUrl/WA1=0   | 
| Pin A2   | baseUrl/A2  | baseUrl/WA2={1..4095} | baseUrl/WA2=0   | 
| Pin A3   | baseUrl/A3  | baseUrl/WA3={1..4095} | baseUrl/WA3=0   |
| Pin A4   | baseUrl/A4  | baseUrl/WA4={1..4095} | baseUrl/WA4=0   |
| Pin A5   | baseUrl/A5  | baseUrl/WA5={1..4095} | baseUrl/WA5=0   | 
| Pin A6   | baseUrl/A5  | baseUrl/WA5={1..4095} | baseUrl/WA5=0   | 
| Pin A7   | baseUrl/A5  | baseUrl/WA5={1..4095} | baseUrl/WA5=0   | 
| DAC      | baseUrl/DAC | baseUrl/WDAC={1..4095} | baseUrl/WDAC=0 |

#### Read Mode 

The Pin Read function consists only of a single request, which can be invoked anytime, returning the value read from the physical Pin. In order to make a continuous reading, the mobile application invokes requests continuously. 

| Pin Name | Get Status  |
| -------- | ------------|
| Pin A0   | baseUrl/A0  |
| Pin A1   | baseUrl/A1  |
| Pin A2   | baseUrl/A2  |
| Pin A3   | baseUrl/A3  |
| Pin A4   | baseUrl/A4  |
| Pin A5   | baseUrl/A5  |
| Pin A6   | baseUrl/A5  |
| Pin A7   | baseUrl/A5  |
| DAC      | baseUrl/DAC |


#### Read/Write response

The responses are common both for Read and Write function, where R- represents read, W – represents write, and NONE indicates no write is going on. 

| Response  JSON                        | Error  JSON                     |
|---------------------------------------|---------------------------------|
| {"A0":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A1":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A2":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A3":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A4":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A5":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A5":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"A5":"'value' "Status":"{W/R/NONE}"} | {"Error":"'Error Description'"} |
| {"DAC":"'value' "Status":"{W/R/NONE}"}| {"Error":"'Error Description'"} |

### RS 232

#### Description

Tx – represents the Rs232 transmitter. If request invoked, the Photon will send the text represented as “Text to send”. Then it will return either ‘Response JSON’ or ‘Error JSON’.
Rx – Represents the RS232 receiver. It consists of two stages. In first stage ‘Request Enable’ enables the receiver to allocate a buffer of the ‘Number’ size. The second stage is receiving the data which have been collected to the allocated buffer.
If the allocation ‘Number’ is greater than 1000, an Error is return: {“Error”:”Buffer too big!”}


|  Name         | Request Enable            | Request to Receive | Response  JSON           | Error  JSON                     |
| ------------- | --------------------------|--------------------|--------------------------|---------------------------------|
|  Tx           | baseUrl/Tx="Text to send" | -                  | {"Tx":"ok"}              | {"Error":"'Error Description'"} |
|  Rx           | baseUrl/Rx=Number         | - baseUrl/Rx=Get   | {"Rx":"Text Received'"}  | {"Error":"'Error Description'"} |


