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
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="08066-104">Communicate with your IoT hub using the MQTT protocol</span><span class="sxs-lookup"><span data-stu-id="08066-104">Communicate with your IoT hub using the MQTT protocol</span></span>
<span data-ttu-id="08066-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span><span class="sxs-lookup"><span data-stu-id="08066-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="08066-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span><span class="sxs-lookup"><span data-stu-id="08066-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="08066-107">Connecting to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="08066-107">Connecting to IoT Hub</span></span>
<span data-ttu-id="08066-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span><span class="sxs-lookup"><span data-stu-id="08066-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="08066-109">Using the device SDKs</span><span class="sxs-lookup"><span data-stu-id="08066-109">Using the device SDKs</span></span>
<span data-ttu-id="08066-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span><span class="sxs-lookup"><span data-stu-id="08066-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="08066-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08066-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="08066-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="08066-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="08066-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08066-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="08066-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08066-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="08066-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="08066-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="08066-116">Language</span><span class="sxs-lookup"><span data-stu-id="08066-116">Language</span></span> | <span data-ttu-id="08066-117">Protocol parameter</span><span class="sxs-lookup"><span data-stu-id="08066-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="08066-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="08066-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="08066-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="08066-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="08066-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="08066-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="08066-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="08066-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="08066-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="08066-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="08066-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="08066-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="08066-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="08066-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="08066-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="08066-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="08066-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="08066-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="08066-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="08066-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="08066-128">Migrating a device app from AMQP to MQTT</span><span class="sxs-lookup"><span data-stu-id="08066-128">Migrating a device app from AMQP to MQTT</span></span>
<span data-ttu-id="08066-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated above.</span><span class="sxs-lookup"><span data-stu-id="08066-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated above.</span></span>

<span data-ttu-id="08066-130">When doing so, make sure to check the following items:</span><span class="sxs-lookup"><span data-stu-id="08066-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="08066-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span><span class="sxs-lookup"><span data-stu-id="08066-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="08066-132">As a result your exception handling logic might require some changes.</span><span class="sxs-lookup"><span data-stu-id="08066-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="08066-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="08066-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="08066-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="08066-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="08066-135">Using the MQTT protocol directly</span><span class="sxs-lookup"><span data-stu-id="08066-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="08066-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="08066-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol.</span></span> <span data-ttu-id="08066-137">In the **CONNECT** packet the device should use the following values:</span><span class="sxs-lookup"><span data-stu-id="08066-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="08066-138">For the **ClientId** field, use the **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="08066-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="08066-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="08066-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="08066-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="08066-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="08066-141">For the **Password** field, use a SAS token.</span><span class="sxs-lookup"><span data-stu-id="08066-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="08066-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span><span class="sxs-lookup"><span data-stu-id="08066-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="08066-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="08066-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="08066-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="08066-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="08066-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span><span class="sxs-lookup"><span data-stu-id="08066-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="08066-146">Go to the **Management** tab in **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="08066-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="08066-147">Click **SAS Token** (top right).</span><span class="sxs-lookup"><span data-stu-id="08066-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="08066-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span><span class="sxs-lookup"><span data-stu-id="08066-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="08066-149">Set your **TTL**.</span><span class="sxs-lookup"><span data-stu-id="08066-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="08066-150">Click **Generate** to create your token.</span><span class="sxs-lookup"><span data-stu-id="08066-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="08066-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="08066-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="08066-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="08066-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="08066-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="08066-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="08066-154">Sending device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="08066-154">Sending device-to-cloud messages</span></span>
<span data-ttu-id="08066-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span><span class="sxs-lookup"><span data-stu-id="08066-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="08066-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span><span class="sxs-lookup"><span data-stu-id="08066-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="08066-157">For example:</span><span class="sxs-lookup"><span data-stu-id="08066-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="08066-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span><span class="sxs-lookup"><span data-stu-id="08066-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="08066-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span><span class="sxs-lookup"><span data-stu-id="08066-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="08066-160">IoT Hub does not support QoS 2 messages.</span><span class="sxs-lookup"><span data-stu-id="08066-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="08066-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span><span class="sxs-lookup"><span data-stu-id="08066-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="08066-162">IoT Hub does not persist Retain messages.</span><span class="sxs-lookup"><span data-stu-id="08066-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="08066-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span><span class="sxs-lookup"><span data-stu-id="08066-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="08066-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span><span class="sxs-lookup"><span data-stu-id="08066-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="08066-165">IoT Hub only supports one active MQTT connection per device.</span><span class="sxs-lookup"><span data-stu-id="08066-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="08066-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span><span class="sxs-lookup"><span data-stu-id="08066-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="08066-167">For more information, see [Messaging developer's guide][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="08066-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="08066-168">Receiving cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="08066-168">Receiving cloud-to-device messages</span></span>
<span data-ttu-id="08066-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span><span class="sxs-lookup"><span data-stu-id="08066-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="08066-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span><span class="sxs-lookup"><span data-stu-id="08066-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="08066-171">IoT Hub does not allow the usage of the **#** or **?**</span><span class="sxs-lookup"><span data-stu-id="08066-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="08066-172">wildcards for filtering of sub-topics.</span><span class="sxs-lookup"><span data-stu-id="08066-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="08066-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span><span class="sxs-lookup"><span data-stu-id="08066-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="08066-174">Note, that the device will not receive any messages from IoT Hub, before it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span><span class="sxs-lookup"><span data-stu-id="08066-174">Note, that the device will not receive any messages from IoT Hub, before it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="08066-175">After successful subscription has been established, the device will start receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span><span class="sxs-lookup"><span data-stu-id="08066-175">After successful subscription has been established, the device will start receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="08066-176">If the device connects with **CleanSession** flag set to **0**, the subscription will be persisted across different sessions.</span><span class="sxs-lookup"><span data-stu-id="08066-176">If the device connects with **CleanSession** flag set to **0**, the subscription will be persisted across different sessions.</span></span> <span data-ttu-id="08066-177">In this case, the next time it connects with **CleanSession 0** the device will receive outstanding messages that have been sent to it while it was disconnected.</span><span class="sxs-lookup"><span data-stu-id="08066-177">In this case, the next time it connects with **CleanSession 0** the device will receive outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="08066-178">If the device uses **CleanSession** flag set to **1** though, it will not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span><span class="sxs-lookup"><span data-stu-id="08066-178">If the device uses **CleanSession** flag set to **1** though, it will not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="08066-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span><span class="sxs-lookup"><span data-stu-id="08066-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="08066-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span><span class="sxs-lookup"><span data-stu-id="08066-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="08066-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span><span class="sxs-lookup"><span data-stu-id="08066-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="08066-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span><span class="sxs-lookup"><span data-stu-id="08066-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="08066-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span><span class="sxs-lookup"><span data-stu-id="08066-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="08066-184">After that, IoT Hub will deliver messages to the device using QoS 1.</span><span class="sxs-lookup"><span data-stu-id="08066-184">After that, IoT Hub will deliver messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="08066-185">Retrieving a device twin's properties</span><span class="sxs-lookup"><span data-stu-id="08066-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="08066-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span><span class="sxs-lookup"><span data-stu-id="08066-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="08066-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. The service will then send a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span><span class="sxs-lookup"><span data-stu-id="08066-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. The service will then send a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="08066-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span><span class="sxs-lookup"><span data-stu-id="08066-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="08066-189">The response body will contain the properties section of the device twin:</span><span class="sxs-lookup"><span data-stu-id="08066-189">The response body will contain the properties section of the device twin:</span></span>

<span data-ttu-id="08066-190">The body of the identity registry entry limited to the “properties” member, for example:</span><span class="sxs-lookup"><span data-stu-id="08066-190">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

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

<span data-ttu-id="08066-191">The possible status codes are:</span><span class="sxs-lookup"><span data-stu-id="08066-191">The possible status codes are:</span></span>

|<span data-ttu-id="08066-192">Status</span><span class="sxs-lookup"><span data-stu-id="08066-192">Status</span></span> | <span data-ttu-id="08066-193">Description</span><span class="sxs-lookup"><span data-stu-id="08066-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="08066-194">200</span><span class="sxs-lookup"><span data-stu-id="08066-194">200</span></span> | <span data-ttu-id="08066-195">Success</span><span class="sxs-lookup"><span data-stu-id="08066-195">Success</span></span> |
| <span data-ttu-id="08066-196">429</span><span class="sxs-lookup"><span data-stu-id="08066-196">429</span></span> | <span data-ttu-id="08066-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="08066-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="08066-198">5\*\*</span><span class="sxs-lookup"><span data-stu-id="08066-198">5\*\*</span></span> | <span data-ttu-id="08066-199">Server errors</span><span class="sxs-lookup"><span data-stu-id="08066-199">Server errors</span></span> |

<span data-ttu-id="08066-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="08066-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="08066-201">Update device twin's reported properties</span><span class="sxs-lookup"><span data-stu-id="08066-201">Update device twin's reported properties</span></span>

<span data-ttu-id="08066-202">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="08066-202">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="08066-203">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08066-203">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="08066-204">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span><span class="sxs-lookup"><span data-stu-id="08066-204">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="08066-205">This message includes a **request id** value.</span><span class="sxs-lookup"><span data-stu-id="08066-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="08066-206">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="08066-206">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="08066-207">This response message uses the same **request id** as the request.</span><span class="sxs-lookup"><span data-stu-id="08066-207">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="08066-208">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span><span class="sxs-lookup"><span data-stu-id="08066-208">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="08066-209">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span><span class="sxs-lookup"><span data-stu-id="08066-209">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="08066-210">A member set to `null`, deletes the member from the containing object.</span><span class="sxs-lookup"><span data-stu-id="08066-210">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="08066-211">For example:</span><span class="sxs-lookup"><span data-stu-id="08066-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="08066-212">The possible status codes are:</span><span class="sxs-lookup"><span data-stu-id="08066-212">The possible status codes are:</span></span>

|<span data-ttu-id="08066-213">Status</span><span class="sxs-lookup"><span data-stu-id="08066-213">Status</span></span> | <span data-ttu-id="08066-214">Description</span><span class="sxs-lookup"><span data-stu-id="08066-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="08066-215">200</span><span class="sxs-lookup"><span data-stu-id="08066-215">200</span></span> | <span data-ttu-id="08066-216">Success</span><span class="sxs-lookup"><span data-stu-id="08066-216">Success</span></span> |
| <span data-ttu-id="08066-217">400</span><span class="sxs-lookup"><span data-stu-id="08066-217">400</span></span> | <span data-ttu-id="08066-218">Bad Request.</span><span class="sxs-lookup"><span data-stu-id="08066-218">Bad Request.</span></span> <span data-ttu-id="08066-219">Malformed JSON</span><span class="sxs-lookup"><span data-stu-id="08066-219">Malformed JSON</span></span> |
| <span data-ttu-id="08066-220">429</span><span class="sxs-lookup"><span data-stu-id="08066-220">429</span></span> | <span data-ttu-id="08066-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="08066-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="08066-222">5\*\*</span><span class="sxs-lookup"><span data-stu-id="08066-222">5\*\*</span></span> | <span data-ttu-id="08066-223">Server errors</span><span class="sxs-lookup"><span data-stu-id="08066-223">Server errors</span></span> |

<span data-ttu-id="08066-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="08066-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="08066-225">Receiving desired properties update notifications</span><span class="sxs-lookup"><span data-stu-id="08066-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="08066-226">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="08066-226">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="08066-227">For example:</span><span class="sxs-lookup"><span data-stu-id="08066-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="08066-228">As for property updates, `null` values means that the JSON object member is being deleted.</span><span class="sxs-lookup"><span data-stu-id="08066-228">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="08066-229">IoT Hub generates change notifications only when devices are connected.</span><span class="sxs-lookup"><span data-stu-id="08066-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="08066-230">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span><span class="sxs-lookup"><span data-stu-id="08066-230">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="08066-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="08066-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="08066-232">Respond to a direct method</span><span class="sxs-lookup"><span data-stu-id="08066-232">Respond to a direct method</span></span>

<span data-ttu-id="08066-233">First, a device has to subscribe to `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="08066-233">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="08066-234">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span><span class="sxs-lookup"><span data-stu-id="08066-234">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="08066-235">To respond, the device will send a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span><span class="sxs-lookup"><span data-stu-id="08066-235">To respond, the device will send a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="08066-236">For more information, see [Direct method developer's guide][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="08066-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="08066-237">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="08066-237">Additional considerations</span></span>
<span data-ttu-id="08066-238">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="08066-238">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="08066-239">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span><span class="sxs-lookup"><span data-stu-id="08066-239">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="08066-240">This approach does require, however, that you run and operate a custom protocol gateway.</span><span class="sxs-lookup"><span data-stu-id="08066-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08066-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="08066-241">Next steps</span></span>
<span data-ttu-id="08066-242">For more information, see [Notes on MQTT support][lnk-mqtt-devguide] in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="08066-242">For more information, see [Notes on MQTT support][lnk-mqtt-devguide] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="08066-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="08066-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="08066-244">To learn more about planning your IoT Hub deployment, see:</span><span class="sxs-lookup"><span data-stu-id="08066-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="08066-245">[Azure Certified for IoT device catalog][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="08066-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="08066-246">[Support additional protocols][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="08066-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="08066-247">[Compare with Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="08066-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="08066-248">[Scaling, HA, and DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="08066-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="08066-249">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="08066-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="08066-250">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="08066-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="08066-251">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="08066-251">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

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
