---
title: include file
description: include file
services: iot-accelerators
author: dominicbetts
ms.service: iot-accelerators
ms.topic: include
ms.date: 07/26/2018
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: dc87079083b8f07ad18f5f871bff64de8d492ebd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45287819"
---
## <a name="the-parts-of-the-device-model-schema"></a><span data-ttu-id="f353b-103">The parts of the device model schema</span><span class="sxs-lookup"><span data-stu-id="f353b-103">The parts of the device model schema</span></span>

<span data-ttu-id="f353b-104">Each device model, such as a chiller or truck, defines a type of device the simulation service can simulate.</span><span class="sxs-lookup"><span data-stu-id="f353b-104">Each device model, such as a chiller or truck, defines a type of device the simulation service can simulate.</span></span> <span data-ttu-id="f353b-105">Each device model is stored in a JSON file with the following top-level schema:</span><span class="sxs-lookup"><span data-stu-id="f353b-105">Each device model is stored in a JSON file with the following top-level schema:</span></span>

```json
{
  "SchemaVersion": "1.0.0",
  "Id": "elevator-01",
  "Version": "0.0.1",
  "Name": "Elevator",
  "Description": "Elevator with floor, vibration and temperature sensors.",
  "Protocol": "AMQP",
  "Simulation": {
    // Specify the simulation behavior
  },
  "Properties": {
    // Define properties
  },
  "Telemetry": [
    // Specify telemetry
  ],
  "CloudToDeviceMethods": {
    // Specify methods
  }
}
```

<span data-ttu-id="f353b-106">You can view the schema files for the default simulated devices in the [devicemodels folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f353b-106">You can view the schema files for the default simulated devices in the [devicemodels folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels) on GitHub.</span></span>

<span data-ttu-id="f353b-107">The following table describes the top-level schema entries:</span><span class="sxs-lookup"><span data-stu-id="f353b-107">The following table describes the top-level schema entries:</span></span>

| <span data-ttu-id="f353b-108">Schema entry</span><span class="sxs-lookup"><span data-stu-id="f353b-108">Schema entry</span></span> | <span data-ttu-id="f353b-109">Description</span><span class="sxs-lookup"><span data-stu-id="f353b-109">Description</span></span> |
| -- | --- |
| `SchemaVersion` | <span data-ttu-id="f353b-110">The schema version is always `1.0.0` and is specific to the format of this file.</span><span class="sxs-lookup"><span data-stu-id="f353b-110">The schema version is always `1.0.0` and is specific to the format of this file.</span></span> |
| `Id` | <span data-ttu-id="f353b-111">A unique ID for this device model.</span><span class="sxs-lookup"><span data-stu-id="f353b-111">A unique ID for this device model.</span></span> |
| `Version` | <span data-ttu-id="f353b-112">Identifies the version of the device model.</span><span class="sxs-lookup"><span data-stu-id="f353b-112">Identifies the version of the device model.</span></span> |
| `Name` | <span data-ttu-id="f353b-113">A friendly name for the device model.</span><span class="sxs-lookup"><span data-stu-id="f353b-113">A friendly name for the device model.</span></span> |
| `Description` | <span data-ttu-id="f353b-114">A description of the device model.</span><span class="sxs-lookup"><span data-stu-id="f353b-114">A description of the device model.</span></span> |
| `Protocol` | <span data-ttu-id="f353b-115">The connection protocol the device uses.</span><span class="sxs-lookup"><span data-stu-id="f353b-115">The connection protocol the device uses.</span></span> <span data-ttu-id="f353b-116">Can be one of `AMQP`, `MQTT`, and `HTTP`.</span><span class="sxs-lookup"><span data-stu-id="f353b-116">Can be one of `AMQP`, `MQTT`, and `HTTP`.</span></span> |

<span data-ttu-id="f353b-117">The following sections describe the other sections in the JSON schema:</span><span class="sxs-lookup"><span data-stu-id="f353b-117">The following sections describe the other sections in the JSON schema:</span></span>

## <a name="simulation"></a><span data-ttu-id="f353b-118">Simulation</span><span class="sxs-lookup"><span data-stu-id="f353b-118">Simulation</span></span>

<span data-ttu-id="f353b-119">In the `Simulation` section, you define the internal state of the simulated device.</span><span class="sxs-lookup"><span data-stu-id="f353b-119">In the `Simulation` section, you define the internal state of the simulated device.</span></span> <span data-ttu-id="f353b-120">Any telemetry values sent by the device must be part of this device state.</span><span class="sxs-lookup"><span data-stu-id="f353b-120">Any telemetry values sent by the device must be part of this device state.</span></span>

<span data-ttu-id="f353b-121">The definition of the device state has two elements:</span><span class="sxs-lookup"><span data-stu-id="f353b-121">The definition of the device state has two elements:</span></span>

* <span data-ttu-id="f353b-122">`InitialState` defines initial values for all the properties of the device state object.</span><span class="sxs-lookup"><span data-stu-id="f353b-122">`InitialState` defines initial values for all the properties of the device state object.</span></span>
* <span data-ttu-id="f353b-123">`Script` identifies a JavaScript file that runs on a schedule to update the device state.</span><span class="sxs-lookup"><span data-stu-id="f353b-123">`Script` identifies a JavaScript file that runs on a schedule to update the device state.</span></span> <span data-ttu-id="f353b-124">You can use this script file to randomize the telemetry values sent by the device.</span><span class="sxs-lookup"><span data-stu-id="f353b-124">You can use this script file to randomize the telemetry values sent by the device.</span></span>

<span data-ttu-id="f353b-125">To learn more about the JavaScript file that updates the device state object, see [Understand the device model behavior](../articles/iot-accelerators/iot-accelerators-device-simulation-device-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f353b-125">To learn more about the JavaScript file that updates the device state object, see [Understand the device model behavior](../articles/iot-accelerators/iot-accelerators-device-simulation-device-behavior.md).</span></span>

<span data-ttu-id="f353b-126">The following example shows the definition of the device state object for a simulated chiller device:</span><span class="sxs-lookup"><span data-stu-id="f353b-126">The following example shows the definition of the device state object for a simulated chiller device:</span></span>

```json
"Simulation": {
  "InitialState": {
    "online": true,
    "temperature": 75.0,
    "temperature_unit": "F",
    "humidity": 70.0,
    "humidity_unit": "%",
    "pressure": 150.0,
    "pressure_unit": "psig",
    "simulation_state": "normal_pressure"
  },
  "Interval": "00:00:10",
  "Scripts": {
    "Type": "javascript",
    "Path": "chiller-01-state.js"
  }
}
```

<span data-ttu-id="f353b-127">The simulation service runs the **chiller-01-state.js** file every five seconds to update the device state.</span><span class="sxs-lookup"><span data-stu-id="f353b-127">The simulation service runs the **chiller-01-state.js** file every five seconds to update the device state.</span></span> <span data-ttu-id="f353b-128">You can see the JavaScript files for the default simulated devices in the [scripts folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f353b-128">You can see the JavaScript files for the default simulated devices in the [scripts folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) on GitHub.</span></span> <span data-ttu-id="f353b-129">By convention, these JavaScript files have the suffix **-state** to distinguish them from the files that implement method behaviors.</span><span class="sxs-lookup"><span data-stu-id="f353b-129">By convention, these JavaScript files have the suffix **-state** to distinguish them from the files that implement method behaviors.</span></span>

## <a name="properties"></a><span data-ttu-id="f353b-130">Properties</span><span class="sxs-lookup"><span data-stu-id="f353b-130">Properties</span></span>

<span data-ttu-id="f353b-131">The `Properties` section of the schema defines the property values the device reports to the solution.</span><span class="sxs-lookup"><span data-stu-id="f353b-131">The `Properties` section of the schema defines the property values the device reports to the solution.</span></span> <span data-ttu-id="f353b-132">For example:</span><span class="sxs-lookup"><span data-stu-id="f353b-132">For example:</span></span>

```json
"Properties": {
  "Type": "Elevator",
  "Location": "Building 2",
  "Latitude": 47.640792,
  "Longitude": -122.126258
}
```

<span data-ttu-id="f353b-133">When the solution starts, it queries all the simulated devices to build a list of `Type` values to use in the UI.</span><span class="sxs-lookup"><span data-stu-id="f353b-133">When the solution starts, it queries all the simulated devices to build a list of `Type` values to use in the UI.</span></span> <span data-ttu-id="f353b-134">The solution uses the `Latitiude` and `Longitude` properties to add the location of the device to the map on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f353b-134">The solution uses the `Latitiude` and `Longitude` properties to add the location of the device to the map on the dashboard.</span></span>

## <a name="telemetry"></a><span data-ttu-id="f353b-135">Telemetry</span><span class="sxs-lookup"><span data-stu-id="f353b-135">Telemetry</span></span>

<span data-ttu-id="f353b-136">The `Telemetry` array lists all the telemetry types the simulated device sends to the solution.</span><span class="sxs-lookup"><span data-stu-id="f353b-136">The `Telemetry` array lists all the telemetry types the simulated device sends to the solution.</span></span>

<span data-ttu-id="f353b-137">The following example sends a JSON telemetry message every 10 seconds with `floor`, `vibration`, and `temperature` data from the elevator's sensors:</span><span class="sxs-lookup"><span data-stu-id="f353b-137">The following example sends a JSON telemetry message every 10 seconds with `floor`, `vibration`, and `temperature` data from the elevator's sensors:</span></span>

```json
"Telemetry": [
  {
    "Interval": "00:00:10",
    "MessageTemplate": "{\"floor\":${floor},\"vibration\":${vibration},\"vibration_unit\":\"${vibration_unit}\",\"temperature\":${temperature},\"temperature_unit\":\"${temperature_unit}\"}",
    "MessageSchema": {
      "Name": "elevator-sensors;v1",
      "Format": "JSON",
      "Fields": {
        "floor": "integer",
        "vibration": "double",
        "vibration_unit": "text",
        "temperature": "double",
        "temperature_unit": "text"
      }
    }
  }
]
```

<span data-ttu-id="f353b-138">`MessageTemplate` defines the structure of the JSON message sent by the simulated device.</span><span class="sxs-lookup"><span data-stu-id="f353b-138">`MessageTemplate` defines the structure of the JSON message sent by the simulated device.</span></span> <span data-ttu-id="f353b-139">The placeholders in `MessageTemplate` use the syntax `${NAME}` where `NAME` is a key from the [device state object](#simulation).</span><span class="sxs-lookup"><span data-stu-id="f353b-139">The placeholders in `MessageTemplate` use the syntax `${NAME}` where `NAME` is a key from the [device state object](#simulation).</span></span> <span data-ttu-id="f353b-140">Strings should be quoted, numbers should not.</span><span class="sxs-lookup"><span data-stu-id="f353b-140">Strings should be quoted, numbers should not.</span></span>

<span data-ttu-id="f353b-141">`MessageSchema` defines the schema of the message sent by the simulated device.</span><span class="sxs-lookup"><span data-stu-id="f353b-141">`MessageSchema` defines the schema of the message sent by the simulated device.</span></span> <span data-ttu-id="f353b-142">The message schema is also published to IoT Hub to enable backend applications to reuse the information to interpret the incoming telemetry.</span><span class="sxs-lookup"><span data-stu-id="f353b-142">The message schema is also published to IoT Hub to enable backend applications to reuse the information to interpret the incoming telemetry.</span></span>

<span data-ttu-id="f353b-143">Currently, you can only use JSON message schemas.</span><span class="sxs-lookup"><span data-stu-id="f353b-143">Currently, you can only use JSON message schemas.</span></span> <span data-ttu-id="f353b-144">The fields listed in the schema can be of the following types:</span><span class="sxs-lookup"><span data-stu-id="f353b-144">The fields listed in the schema can be of the following types:</span></span>

* <span data-ttu-id="f353b-145">Object - serialized using JSON</span><span class="sxs-lookup"><span data-stu-id="f353b-145">Object - serialized using JSON</span></span>
* <span data-ttu-id="f353b-146">Binary - serialized using base64</span><span class="sxs-lookup"><span data-stu-id="f353b-146">Binary - serialized using base64</span></span>
* <span data-ttu-id="f353b-147">Text</span><span class="sxs-lookup"><span data-stu-id="f353b-147">Text</span></span>
* <span data-ttu-id="f353b-148">Boolean</span><span class="sxs-lookup"><span data-stu-id="f353b-148">Boolean</span></span>
* <span data-ttu-id="f353b-149">Integer</span><span class="sxs-lookup"><span data-stu-id="f353b-149">Integer</span></span>
* <span data-ttu-id="f353b-150">Double</span><span class="sxs-lookup"><span data-stu-id="f353b-150">Double</span></span>
* <span data-ttu-id="f353b-151">DateTime</span><span class="sxs-lookup"><span data-stu-id="f353b-151">DateTime</span></span>

<span data-ttu-id="f353b-152">To send telemetry messages at different intervals, add multiple telemetry types to the `Telemetry` array.</span><span class="sxs-lookup"><span data-stu-id="f353b-152">To send telemetry messages at different intervals, add multiple telemetry types to the `Telemetry` array.</span></span> <span data-ttu-id="f353b-153">The following example sends temperature and humidity data every 10 seconds and the state of the light every minute:</span><span class="sxs-lookup"><span data-stu-id="f353b-153">The following example sends temperature and humidity data every 10 seconds and the state of the light every minute:</span></span>

```json
"Telemetry": [
  {
    "Interval": "00:00:10",
    "MessageTemplate":
      "{\"temperature\":${temperature},\"temperature_unit\":\"${temperature_unit}\",\"humidity\":\"${humidity}\"}",
    "MessageSchema": {
      "Name": "RoomComfort;v1",
      "Format": "JSON",
      "Fields": {
        "temperature": "double",
        "temperature_unit": "text",
        "humidity": "integer"
      }
    }
  },
  {
    "Interval": "00:01:00",
    "MessageTemplate": "{\"lights\":${lights_on}}",
    "MessageSchema": {
      "Name": "RoomLights;v1",
      "Format": "JSON",
      "Fields": {
        "lights": "boolean"
      }
    }
  }
],
```

## <a name="cloudtodevicemethods"></a><span data-ttu-id="f353b-154">CloudToDeviceMethods</span><span class="sxs-lookup"><span data-stu-id="f353b-154">CloudToDeviceMethods</span></span>

<span data-ttu-id="f353b-155">A simulated device can respond to cloud-to-device methods called from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f353b-155">A simulated device can respond to cloud-to-device methods called from an IoT hub.</span></span> <span data-ttu-id="f353b-156">The `CloudToDeviceMethods` section in the device model schema file:</span><span class="sxs-lookup"><span data-stu-id="f353b-156">The `CloudToDeviceMethods` section in the device model schema file:</span></span>

* <span data-ttu-id="f353b-157">Defines the methods the simulated device can respond to.</span><span class="sxs-lookup"><span data-stu-id="f353b-157">Defines the methods the simulated device can respond to.</span></span>
* <span data-ttu-id="f353b-158">Identifies the JavaScript file that contains the logic to execute.</span><span class="sxs-lookup"><span data-stu-id="f353b-158">Identifies the JavaScript file that contains the logic to execute.</span></span>

<span data-ttu-id="f353b-159">The simulated device sends the list of methods it supports to the IoT hub it's connected to.</span><span class="sxs-lookup"><span data-stu-id="f353b-159">The simulated device sends the list of methods it supports to the IoT hub it's connected to.</span></span>

<span data-ttu-id="f353b-160">To learn more about the JavaScript file that implements the behavior of the device, see [Understand the device model behavior](../articles/iot-accelerators/iot-accelerators-device-simulation-device-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f353b-160">To learn more about the JavaScript file that implements the behavior of the device, see [Understand the device model behavior](../articles/iot-accelerators/iot-accelerators-device-simulation-device-behavior.md).</span></span>

<span data-ttu-id="f353b-161">The following example specifies three supported methods and the JavaScript files that implement those methods:</span><span class="sxs-lookup"><span data-stu-id="f353b-161">The following example specifies three supported methods and the JavaScript files that implement those methods:</span></span>

```json
"CloudToDeviceMethods": {
  "Reboot": {
    "Type": "javascript",
    "Path": "Reboot-method.js"
  },
  "EmergencyValveRelease": {
    "Type": "javascript",
    "Path": "EmergencyValveRelease-method.js"
  },
  "IncreasePressure": {
    "Type": "javascript",
    "Path": "IncreasePressure-method.js"
  }
}
```

<span data-ttu-id="f353b-162">You can see the JavaScript files for the default simulated devices in the [scripts folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f353b-162">You can see the JavaScript files for the default simulated devices in the [scripts folder](https://github.com/Azure/device-simulation-dotnet/tree/master/Services/data/devicemodels/scripts) on GitHub.</span></span> <span data-ttu-id="f353b-163">By convention, these JavaScript files have the suffix **-method** to distinguish them from the files that implement state behavior.</span><span class="sxs-lookup"><span data-stu-id="f353b-163">By convention, these JavaScript files have the suffix **-method** to distinguish them from the files that implement state behavior.</span></span>