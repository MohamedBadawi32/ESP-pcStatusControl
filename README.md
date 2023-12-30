# ESP-pcStatusControl

Lately I got my hands on ESP and it has been fun!

I have designed a simple circuit to control the status of my PC remotely. In simple terms, the PC can be turned on via a webpage that is accessible worldwide.

## Project Aims:
1. Controlling the status of the PC remotely.
2. Maintaining the PC push button function.

## Project Needs:
1. Online server.
2. ESP32 with Wi-Fi capability.
3. Power source.

### Project Needs: Online Server
I used 000webhost as it's easy to comprehend, free, and responsive. All I had to do, besides uploading PHP files for the webpage design, is to create database with a single row table that will be checked and altered by the ESP.

### Project Needs: ESP32 with Wi-Fi Capabilities
1. ESP selection:
Initially I started with "38-pin ESP32 WROOM 32" but it turned out to be superfluous. Alternatively, I used ESP32-C3 Supermini which as the name describes it, supermini and superb!

Note: You can find "ESP32-01S" attached to a relay and sold as a module, however, it needs a separate programmer, and it lacks 5 volts pin.

2. ESP programming & operation:
The ESP communicates with the server database periodically with a 1 min delay. If the webpage button is pressed:
- The status in the server database changes to 1.
- The ESP detects the change and sends a HIGH signal for half a second energizing the relay which shorts the PC Power Pins together to turn it on.
- The ESP changes the status in the database to 0.

Most importantly, the button function is preserved away from any server or ESP failures. The button simply allows 3.3 volts from the ESP to energize the relay module directly. (Avoid using the 5 volts line as ESP operates on 3.3 volts)

### Project Needs: Power Source
Surprisingly, the USB on computer motherboards can be left on AFTER a shutdown! The feature can be accessed through the Control Panel>Hardware and Sound>Power Options>Change plan settings (of your selected)>Change advanced power settings>USB settings>USB selective suspend settings.
Taking advantage of this, 5 volts and ground are extended from any vacant USB headers and fed into the ESP and relay module.


Finally, the relay module is redundant, however, removing it will get me into the risk of sending direct signals to the motherboard from a cheap AliExpress product (ESP). If the ESP is from a well-known brand, a HIGH signal from a digital pin will be directly connected to the 3.3 volts PC Power Pin so that the PC turns on once a LOW signal is present on the pin. The push button will retain its operation of bringing the 3.3 volts PC Power Pin to ground to turn it on.
