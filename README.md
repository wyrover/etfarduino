etfarduino
==========

A project which allows the use of an Arduino device for data acquisition within the MATLAB Data Acquisition Toolbox.

It was developed as a part of my Bachelor's thesis which I completed at the Faculty of Electrical Engineering Sarajevo
(www.etf.unsa.ba/)

The project is published under the MIT license.

Download
--------

The compiled binaries can be found in the [Downloads section](https://github.com/mlalic/etfarduino/downloads).

Components
----------

The project contains four components which work together to achieve the goal of using Arduino for data acquisition
from within MATLAB.

1. EtfArduinoFirmware -- an Arduino sketch which allows it to respond to commands from the computer;
2. EtfArduinoService -- a service process which allows its client processes to access Arduino's data acquisition functionality. This way, it is possible to develop other applications relying on this functionality;
3. etfarduino.dll -- a DLL which implements the adaptor COM interface for MATLAB's Data Acquisition Toolbox;
4. EtfArduinoConfig -- a GUI application for configuring connected Arduino devices for data acquisition.

Usage
-----

To use this software follow these steps:
- Compile and upload the Arduino sketch (EtfArduinoFirmware) using the Arduino IDE;
- Start the EtfArduinoService.exe application;
- Register the adaptor in the MATLAB environment by running the command `daqregister 'path/to/etfarduino.dll'`;
- Run the EtfArduinoConfig application and register the connected Arduino as an acquisition device by clicking the button.

It is now possible to use the connected Arduino device as any other acquisition device, such as MCC or National Instruments
devices.

For example:

    ai = analoginput('etfarduino', 0);
    addchannel(ai, 0);
    start(ai);
    wait(ai, 2);
    [data, t] = getdata(ai, ai.SampleAcquired);
    plot(t, data)

Notes
-----

Currently, only one analog input and analog output channel is supported and they use the A0 pin and digital pin 3, respectively. Analog input and output can work in parallel.

Using the EtfArduinoConfig it is possible to register multiple Arduino boards which are able to perform acquisition tasks in parallel.