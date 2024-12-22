# one-key
An App that brings all your digital wireless keys together to one platform.

## Idea Description 
Having one app to hold all your RFID and NFC Signals Rather than having to carry them around with you everywhere and forgetting about them.

## Limitations and Requirements
Apple Does not allow NFC/RFID transmission withuot Apple Pay.
Having Multiple Copies and Distrubuting Security Keys is illegal.
Maintaining a small formfactor for ease of use. 

## Proposed Solution
Using a bluetooh module embedded in a lightweight formfactor like a case. That would communicate to a module that would emulate the RFID/NFC Signals that are stored within the app on the users account, upon entering or registering the key, the key on the signal must be deleted to prevent mass distrubution of the security keys. 

## Technicals:
For the microcontroller, the ESP32 would be an excellent foundation. Here's why:

It has built-in Bluetooth Low Energy and WiFi capabilities
There's extensive documentation and community support
It's relatively inexpensive and easy to work with
Many NFC/RFID modules are designed to work seamlessly with it
It has plenty of processing power for this application
The Arduino framework supports it, making development easier

For the NFC/RFID functionality, you could use the PN532 module, which is well-documented and can handle both reading and emulation. This is actually the same chip used in many commercial NFC readers and the Flipper Zero.
Regarding the Flipper Zero's open source code - yes, this could be extremely valuable! Their GitHub repository contains:

The core NFC/RFID communication protocols
Signal processing algorithms
Bluetooth communication handling
Power management strategies

You wouldn't want to copy their code directly, but studying how they implemented these features could give you excellent insights for your own implementation. Pay particular attention to:

How they handle different NFC/RFID protocols
Their Bluetooth communication architecture
Their power management approach
Their signal processing techniques

For development, I'd recommend starting with:

The Arduino IDE or PlatformIO for ESP32 development
The NFC/RFID libraries for Arduino (especially for the PN532)
The ESP32 BLE libraries for Bluetooth communication


The ST25R3916 is actually an excellent choice for your project - potentially even better than the PN532 I mentioned earlier. Let me explain why and how it could work in your design.
The ST25R3916 is a highly integrated NFC reader IC that offers several advantages specifically relevant to your case design:
Its size and integration level make it particularly suitable for a thin phone case design. While the PN532 requires more external components, the ST25R3916 integrates many necessary functions into a single chip, including:

The analog front-end
The digital signal processing
The protocol handling
Wave shaping capabilities
Automatic antenna tuning

It supports multiple protocols that would be useful for your application:

NFC-A, NFC-B, and NFC-F protocols
ISO/IEC 14443A and B
ISO/IEC 15693
FeliCa
Low-power card detection

What makes it especially suitable for your project is its built-in EMD (Easy Mismatch Detector) feature, which helps optimize the antenna matching automatically. This is crucial when working with a confined space like a phone case where antenna placement might not be ideal.
You could pair this with an ESP32-PICO-D4 for an extremely compact solution. The ST25R3916 would handle all the NFC operations while the ESP32 manages:

The Bluetooth communication with the phone
The user interface control
The credential storage and management
The power management system

The communication between the ESP32 and ST25R3916 would be via SPI, which is efficient and requires minimal connections. This helps keep the PCB layout compact.
Would you like me to elaborate on how you might set up the initial development environment for working with this chip? Or shall we discuss specific antenna design considerations for optimal performance in a phone case form factor?
