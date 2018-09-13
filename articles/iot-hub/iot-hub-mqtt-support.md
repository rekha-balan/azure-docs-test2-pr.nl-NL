---
title: Understand Azure IoT Hub MQTT support | Microsoft Docs
description: Developer guide - support for devices connecting to an IoT Hub device-facing endpoint using the MQTT protocol. Includes information about built-in MQTT support in the Azure IoT device SDKs.
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: ''
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7b9b7e558a95de88dedcb744e2a4b3c18cde35cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551340"
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a>Communicate with your IoT hub using the MQTT protocol
IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443. IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).

## <a name="connecting-to-iot-hub"></a>Connecting to IoT Hub
A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.

## <a name="using-the-device-sdks"></a>Using the device SDKs
[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python. The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub. To use the MQTT protocol, the client protocol parameter must be set to **MQTT**. By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.

When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.

The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.

| Language | Protocol parameter |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a>Migrating a device app from AMQP to MQTT
If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated above.

When doing so, make sure to check the following items:

* AMQP returns errors for many conditions, while MQTT terminates the connection. As a result your exception handling logic might require some changes.
* MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging]. If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].

## <a name="using-the-mqtt-protocol-directly"></a>Using the MQTT protocol directly
If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol. In the **CONNECT** packet the device should use the following values:

* For the **ClientId** field, use the **deviceId**.
* For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.

    For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* For the **Password** field, use a SAS token. The format of the SAS token is the same as for both the HTTP and AMQP protocols:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].

    When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:

  1. Go to the **Management** tab in **Device Explorer**.
  2. Click **SAS Token** (top right).
  3. On **SASTokenForm**, select your device in the **DeviceID** drop down. Set your **TTL**.
  4. Click **Generate** to create your token.

     The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.

### <a name="sending-device-to-cloud-messages"></a>Sending device-to-cloud messages
After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**. The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format. For example:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.
>
>

The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.

- IoT Hub does not support QoS 2 messages. If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.
- IoT Hub does not persist Retain messages. If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message. In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.
- IoT Hub only supports one active MQTT connection per device. Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.

For more information, see [Messaging developer's guide][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Receiving cloud-to-device messages
To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**. The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name. IoT Hub does not allow the usage of the **#** or **?** wildcards for filtering of sub-topics. Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.

Note, that the device will not receive any messages from IoT Hub, before it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter. After successful subscription has been established, the device will start receiving only cloud-to-device messages that have been sent to it after the time of the subscription. If the device connects with **CleanSession** flag set to **0**, the subscription will be persisted across different sessions. In this case, the next time it connects with **CleanSession 0** the device will receive outstanding messages that have been sent to it while it was disconnected. If the device uses **CleanSession** flag set to **1** though, it will not receive any messages from IoT Hub until it subscribes to its device-endpoint.

IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties. `{property_bag}` contains url-encoded key/value pairs of message properties. Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag. System property names have the prefix **$**, application properties use the original property name with no prefix.

When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet. After that, IoT Hub will deliver messages to the device using QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Retrieving a device twin's properties

First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses. Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. The service will then send a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.

Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.
The response body will contain the properties section of the device twin:

The body of the identity registry entry limited to the “properties” member, for example:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

The possible status codes are:

|Status | Description |
| ----- | ----------- |
| 200 | Success |
| 429 | Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas] |
| 5** | Server errors |

For more information, see [Device twins developer's guide][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Update device twin's reported properties

The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:

1. A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.

1. A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic. This message includes a **request id** value.

1. The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`. This response message uses the same **request id** as the request.

The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).
Each member in the JSON document updates or add the corresponding member in the device twin’s document. A member set to `null`, deletes the member from the containing object. For example:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

The possible status codes are:

|Status | Description |
| ----- | ----------- |
| 200 | Success |
| 400 | Bad Request. Malformed JSON |
| 429 | Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas] |
| 5** | Server errors |

For more information, see [Device twins developer's guide][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Receiving desired properties update notifications

When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end. For example:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

As for property updates, `null` values means that the JSON object member is being deleted.


> [!IMPORTANT] 
> IoT Hub generates change notifications only when devices are connected. Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.

For more information, see [Device twins developer's guide][lnk-devguide-twin].

### <a name="respond-to-a-direct-method"></a>Respond to a direct method

First, a device has to subscribe to `$iothub/methods/POST/#`. IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.

To respond, the device will send a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.

For more information, see [Direct method developer's guide][lnk-methods].

### <a name="additional-considerations"></a>Additional considerations
As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub. The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols. This approach does require, however, that you run and operate a custom protocol gateway.

## <a name="next-steps"></a>Next steps
For more information, see [Notes on MQTT support][lnk-mqtt-devguide] in the IoT Hub developer guide.

To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].

To learn more about planning your IoT Hub deployment, see:

* [Azure Certified for IoT device catalog][lnk-devices]
* [Support additional protocols][lnk-protocols]
* [Compare with Event Hubs][lnk-compare]
* [Scaling, HA, and DR][lnk-scaling]

To further explore the capabilities of IoT Hub, see:

* [IoT Hub developer guide][lnk-devguide]
* [Simulating a device with the IoT Gateway SDK][lnk-gateway]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-mqtt-devguide]: iot-hub-devguide-messaging.md#notes-on-mqtt-support
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
