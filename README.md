# WeConnect-mycupra-mqtt

This is a simple fork of the excellent implementation for Volkswagen Cars by Till Steinbach [WeConnect-mqtt](https://github.com/tillsteinbach/WeConnect-mqtt)
that uses the fork of the underlying library to work with the Cupra ["cupra_we_connect"](https://github.com/daernsinstantfortress/cupra_we_connect).

[MQTT](https://mqtt.org) Client that publishes data from Cupra MyCupra Services

## What is the purpose?
If you want to integrate data from your weconnect enabled car a standard protocol such as [MQTT](https://mqtt.org) can be very helpful. This Client enables you to integrate with the [MQTT Broker](https://mqtt.org/software/) of your choice (e.g. your home automation solution such as [ioBroker](https://www.iobroker.net), [FHEM](https://fhem.de) or [Home Assistant](https://www.home-assistant.io))

## Requirements
You need to install python 3 on your system: [How to install python](https://realpython.com/installing-python/). The minimum required python version is 3.8

### Login & Consent
WeConnect-mqtt is based on the new WeConnect/Cupra API that was introduced with the new series of ID cars. If you use another car or hybrid you probably need to agree to the terms and conditions of the new WeConnect interface. Easiest to do so is by installing the Volkswagen app on your smartphone and login there. If necessary you will be asked to agree to the terms and conditions.

## How to use
Start weconnect-mqtt from the commandline:
```bash
weconnect-mqtt
```
You get all the usage information by using the --help command
```bash
weconnect-mqtt --help
```
An example to connect with an MQTT broker at 192.168.0.1 with user test and password test123 is
```bash
weconnect-mqtt --username test@test.de --password test123 --mqttbroker 192.168.0.1 --mqtt-username test --mqtt-password test123 --prefix weconnect
```
The client uses user test@test.de and password test123 in this example to connect to weconnect

### Credentials
If you do not want to provide your username or password all the time you have to create a ".netrc" file at the appropriate location (usually this is your home folder):
```
# For WeConnect
machine volkswagen.de
login test@test.de
password testpassword123

# For the MQTTBroker
machine 192.168.0.1
login test
password testpassword123
```
You can also provide the location of the netrc file using the --netrc option

### Charging stations
You can also obtain data from charging stations by adding a location with e.g. `--chargingLocation 52.437132 10.796628` and a radius in meters with `--chargingLocationRadius=500`.
Data for charging stations is mostly static, but you can see the current availability.

### Topics
If your broker does not let you observe all available topics you can pass the parameter `--list-topics` to get all topics displayed on the commandline. Topics marked as "(writeable)" can be manipulated.
There are also two topics to receive all available topics as a comma seperated list: `weconnect/0/mqtt/topics` lists all available topics, `weconnect/0/mqtt/writeableTopics` provides topics that can be manipulated.

### Disabling features
You can disable data for the cars capabilities with `--no-capabilities`
If you only need a subset of the data you can use the `--selective` option. E.g. `--selective climatisation`

### Images
You can enable ASCII Art pictures of the cars with `--pictures`

#### PNG vehicle images
If your client can deal with PNG-images received through MQTT you can set `--picture-format png`

### Times
By default the times coming from the car are UTC isoformat. You can convert times to your local timezone by adding `--convert-times`. Convert times will use the systems timezone. If you want to set a specific timezone use e.g. `--convert-times Europe/Berlin`.
You can format times in your local format by adding `--timeformat`. This will use the default Date/Time format of your locale setting. If you want to set a specific format use e.g. `--timeformat '%a %d %b %Y %T'`.
If you want to set the date in another language than default on your system use e.g. `--locale de_DE`.

### Raw JSON
If you want to continue working with the whole data you can also enable the topic `weconnect/0/rawjson` by adding `--with-raw-json-topic`. The topic is published on every change of the json string.

## Tested with
- Cupra Born model year 2022

## Reporting Issues
Please feel free to open an issue at [GitHub Issue page](https://github.com/tillsteinbach/WeConnect-mqtt/issues) to report problems you found.

## More Questions?
Please see the wiki [Wiki](https://github.com/tillsteinbach/WeConnect-mqtt/wiki) or start a [discussion](https://github.com/tillsteinbach/WeConnect-mqtt/discussions).

### Known Issues
- The Tool is in alpha state and may change unexpectedly at any time!

## Related Projects:
- [cupra_we_connect](https://github.com/daernsinstantfortress/cupra_we_connect): Python API to connect to the Cupra WeConnect Services
