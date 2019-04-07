*Quick links :*
[Home](/README.md) - [Part 1](/part1/README.md) - [**Part 2**](/part2/README.md) - [Part 3](/part3/README.md)
***
**Part 2** - [Device Registration](/part2/DEVICE.md) - [**Application**](/part2/APP.md)
***

# Creating the sensing application for the Raspberry Pi

## Lab Objectives

In this lab you will pull together all the information from part 1 into a single app.  You will learn:

- Use the SenseHAT nodes to get environmental data
- Work with the IoT platform using the Watson IoT nodes
- How to work with JSON data in Node-RED

## Watson IoT nodes

On the Raspberry Pi the Watson IoT nodes are pre-installed.  You can use them to connect to the IoT platform as a device or gateway.  On Node-RED deployed to the IBM Cloud via the starter kit the IoT nodes connect as an application.

The Watson IoT nodes will connect to the Watson IoT platform using SSL/TLS connection and have the default server certificate for the IoT platform included in the node.  

Open the node configuration, then create a new connection configuration.  You want to connect as a registered device, then enter the details for your org, device type, device ID and security token (used when registering the device on the IoT platform).

Close the configuration and deploy the changes, you should see the node change to connected status.  You can also check the IoT platform console and see the device is connected.

Use an Inject node to send a JSON payload to the IoT platform.  Check on the IoT platform console to see the data arrive.

## Node-RED flow

Create a Node-RED flow to send environment data to the Internet of Things platform.  You should use the following format to send the data to the platform:

``` json
{
  "d" : {
    "temp" : temp
  }
}
```

where temp and hum are numbers from the live environment data.

``` json
[{"id":"9c4f14b7.2f1e58","type":"template","z":"2052228e.805f0e","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"{\"d\" : {\"temp\" : {{payload}}\n        }\n}","output":"json","x":440,"y":220,"wires":[["9af199e9.fb3378"]]},{"id":"9af199e9.fb3378","type":"debug","z":"2052228e.805f0e","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":610,"y":140,"wires":[]},{"id":"4695d081.10277","type":"inject","z":"2052228e.805f0e","name":"","topic":"","payload":"","payloadType":"date","repeat":"30","crontab":"","once":false,"onceDelay":0.1,"x":110,"y":220,"wires":[["286983e8.f2dfbc"]]},{"id":"286983e8.f2dfbc","type":"rpi-dht22","z":"2052228e.805f0e","name":"","topic":"rpi-dht22","dht":22,"pintype":"0","pin":4,"x":280,"y":220,"wires":[["9c4f14b7.2f1e58"]]}]
```

As an additional step only send data to the IoT platform every 30 seconds, but ensure you send the latest data and discard the intermediate values.

***
*Quick links :*
[Home](/README.md) - [Part 1](/part1/README.md) - [**Part 2**](/part2/README.md) - [Part 3](/part3/README.md)
