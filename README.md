This code configures an ESP32 device to act as a Bluetooth Low Energy (BLE) server, which advertises two services: one for temperature measurement and another for humidity measurement. The device broadcasts these services and allows connected clients to read the values and receive notifications when the values change.

Detailed Description
BLE Initialization:

The code begins by initializing the serial communication for debugging purposes with Serial.begin(115200).
It then initializes the BLE functionality on the ESP32 using BLEDevice::init("ESP32_BLE"), which sets the device name to "ESP32_BLE".
Creating BLE Server and Service:

A BLE server is created with BLEDevice::createServer().
A BLE service is defined and created with a unique service UUID (SERVICE_UUID).
Creating Characteristics:

Two characteristics are created for the service:
Temperature characteristic with UUID CHARACTERISTIC_UUID_TEMP.
Humidity characteristic with UUID CHARACTERISTIC_UUID_HUM.
These characteristics are configured to support reading and notifying connected clients of changes (BLECharacteristic::PROPERTY_READ | BLECharacteristic::PROPERTY_NOTIFY).
Adding Descriptors:

Each characteristic is assigned a descriptor (BLE2902) that allows notifications to be enabled by the client.
Setting Initial Values:

Initial values for the temperature and humidity characteristics are set to "25.0" and "50.0" respectively, representing default temperature and humidity readings.
Starting the Service and Advertising:

The BLE service is started with pService->start().
The server starts advertising its presence to potential clients with pServer->getAdvertising()->start().
Simulating Sensor Readings:

In the loop() function, the code simulates sensor readings for temperature and humidity every 5 seconds.
Random values are generated to represent temperature (between 20.0°C and 30.0°C) and humidity (between 40.0% and 60.0%).
These values are updated in the corresponding BLE characteristics using pCharacteristicTemp->setValue(String(temperature).c_str()) and pCharacteristicHum->setValue(String(humidity).c_str()).
Notifications are sent to connected clients using pCharacteristicTemp->notify() and pCharacteristicHum->notify().
