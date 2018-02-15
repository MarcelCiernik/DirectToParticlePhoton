# DirectToParticlePhoton
DirectToParticlePhoton is an open source software for Particle. It allows to connect Particle Photon wirelessly __without necessity to use internet__ and __without need to have Particle Account__ (to be able to build and flas the device), from Android device, IOs Device or Microsoft mobile device. 

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

## Compile and Build source with Eclipse IDE

## Compile and Build source with Eclipse IDE

## DirectToParticlePhoton http services published

DirectToParticle application is http based, and all the individual functionality are triggered by a request.
The request/response list:

| Pin Name      | Request Enable  | Request Disable  | Error  JSON                    |
| ------------- | ----------------|------------------|--------------------------------|
| Pin D0        | baseUrl/D0=true | baseUrl/D0=false | {"Error":"{Error Description}" |
| Pin D1        | baseUrl/D1=true | baseUrl/D1=false | {"Error":"{Error Description}" |
| Pin D2        | baseUrl/D2=true | baseUrl/D2=false | {"Error":"{Error Description}" |
| Pin D3        | baseUrl/D3=true | baseUrl/D3=false | {"Error":"{Error Description}" |
| Pin D4        | baseUrl/D4=true | baseUrl/D4=false | {"Error":"{Error Description}" |
| Pin D5        | baseUrl/D5=true | baseUrl/D5=false | {"Error":"{Error Description}" |
| Pin D6        | baseUrl/D6=true | baseUrl/D6=false | {"Error":"{Error Description}" |
| Pin D7        | baseUrl/D7=true | baseUrl/D7=false | {"Error":"{Error Description}" |

