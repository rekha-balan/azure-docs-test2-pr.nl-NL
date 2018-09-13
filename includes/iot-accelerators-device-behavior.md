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
ms.openlocfilehash: cb1392bd70c92ae4f6bfc6707198c3079ad7ecef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856261"
---
## <a name="state-behavior"></a><span data-ttu-id="bd38f-103">State behavior</span><span class="sxs-lookup"><span data-stu-id="bd38f-103">State behavior</span></span>

<span data-ttu-id="bd38f-104">The [Simulation](../articles/iot-accelerators/iot-accelerators-device-simulation-device-schema.md#simulation) section of the device model schema defines the internal state of a simulated device:</span><span class="sxs-lookup"><span data-stu-id="bd38f-104">The [Simulation](../articles/iot-accelerators/iot-accelerators-device-simulation-device-schema.md#simulation) section of the device model schema defines the internal state of a simulated device:</span></span>

- <span data-ttu-id="bd38f-105">`InitialState` defines initial values for all the properties of the device state object.</span><span class="sxs-lookup"><span data-stu-id="bd38f-105">`InitialState` defines initial values for all the properties of the device state object.</span></span>
- <span data-ttu-id="bd38f-106">`Script` identifies a JavaScript file that runs on a schedule to update the device state.</span><span class="sxs-lookup"><span data-stu-id="bd38f-106">`Script` identifies a JavaScript file that runs on a schedule to update the device state.</span></span>

<span data-ttu-id="bd38f-107">The following example shows the definition of the device state object for a simulated chiller device:</span><span class="sxs-lookup"><span data-stu-id="bd38f-107">The following example shows the definition of the device state object for a simulated chiller device:</span></span>

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
  "Interval": "00:00:05",
  "Scripts": {
    "Type": "javascript",
    "Path": "chiller-01-state.js"
  }
}
```

<span data-ttu-id="bd38f-108">The state of the simulated device, as defined in the `InitialState` section, is held in memory by the simulation service.</span><span class="sxs-lookup"><span data-stu-id="bd38f-108">The state of the simulated device, as defined in the `InitialState` section, is held in memory by the simulation service.</span></span> <span data-ttu-id="bd38f-109">The state information is passed as input to the `main` function defined in **chiller-01-state.js**.</span><span class="sxs-lookup"><span data-stu-id="bd38f-109">The state information is passed as input to the `main` function defined in **chiller-01-state.js**.</span></span> <span data-ttu-id="bd38f-110">In this example, the simulation service runs the **chiller-01-state.js** file every five seconds.</span><span class="sxs-lookup"><span data-stu-id="bd38f-110">In this example, the simulation service runs the **chiller-01-state.js** file every five seconds.</span></span> <span data-ttu-id="bd38f-111">The script can modify the state of the simulated device.</span><span class="sxs-lookup"><span data-stu-id="bd38f-111">The script can modify the state of the simulated device.</span></span>

<span data-ttu-id="bd38f-112">The following shows the outline of a typical `main` function:</span><span class="sxs-lookup"><span data-stu-id="bd38f-112">The following shows the outline of a typical `main` function:</span></span>

```javascript
function main(context, previousState, previousProperties) {

  // Use the previous device state to
  // generate the new device state
  // returned by the function.

  return state;
}
```

<span data-ttu-id="bd38f-113">The `context` parameter has the following properties:</span><span class="sxs-lookup"><span data-stu-id="bd38f-113">The `context` parameter has the following properties:</span></span>

- <span data-ttu-id="bd38f-114">`currentTime` as a string with format `yyyy-MM-dd'T'HH:mm:sszzz`</span><span class="sxs-lookup"><span data-stu-id="bd38f-114">`currentTime` as a string with format `yyyy-MM-dd'T'HH:mm:sszzz`</span></span>
- <span data-ttu-id="bd38f-115">`deviceId`, for example `Simulated.Chiller.123`</span><span class="sxs-lookup"><span data-stu-id="bd38f-115">`deviceId`, for example `Simulated.Chiller.123`</span></span>
- <span data-ttu-id="bd38f-116">`deviceModel`, for example `Chiller`</span><span class="sxs-lookup"><span data-stu-id="bd38f-116">`deviceModel`, for example `Chiller`</span></span>

<span data-ttu-id="bd38f-117">The `state` parameter contains the state of the device as maintained by the device simulation service.</span><span class="sxs-lookup"><span data-stu-id="bd38f-117">The `state` parameter contains the state of the device as maintained by the device simulation service.</span></span> <span data-ttu-id="bd38f-118">This value is the `state` object returned by the previous call to `main`.</span><span class="sxs-lookup"><span data-stu-id="bd38f-118">This value is the `state` object returned by the previous call to `main`.</span></span>

<span data-ttu-id="bd38f-119">The following example shows a typical implementation of the `main` method to handle the device state maintained by the simulation service:</span><span class="sxs-lookup"><span data-stu-id="bd38f-119">The following example shows a typical implementation of the `main` method to handle the device state maintained by the simulation service:</span></span>

```javascript
// Default state
var state = {
  online: true,
  temperature: 75.0,
  temperature_unit: "F",
  humidity: 70.0,
  humidity_unit: "%",
  pressure: 150.0,
  pressure_unit: "psig",
  simulation_state: "normal_pressure"
};

function restoreState(previousState) {
  // If the previous state is null, force a default state
  if (previousState !== undefined && previousState !== null) {
      state = previousState;
  } else {
      log("Using default state");
  }
}

function main(context, previousState, previousProperties) {

  restoreState(previousState);

  // Update state

  return state;
}
```

<span data-ttu-id="bd38f-120">The following example shows how the `main` method can simulate telemetry values that vary over time:</span><span class="sxs-lookup"><span data-stu-id="bd38f-120">The following example shows how the `main` method can simulate telemetry values that vary over time:</span></span>

```javascript
/**
 * Simple formula generating a random value
 * around the average and between min and max
 */
function vary(avg, percentage, min, max) {
  var value = avg * (1 + ((percentage / 100) * (2 * Math.random() - 1)));
  value = Math.max(value, min);
  value = Math.min(value, max);
  return value;
}


function main(context, previousState, previousProperties) {

    restoreState(previousState);

    // 75F +/- 5%,  Min 25F, Max 100F
    state.temperature = vary(75, 5, 25, 100);

    // 70% +/- 5%,  Min 2%, Max 99%
    state.humidity = vary(70, 5, 2, 99);

    log("Simulation state: " + state.simulation_state);
    if (state.simulation_state === "high_pressure") {
        // 250 psig +/- 25%,  Min 50 psig, Max 300 psig
        state.pressure = vary(250, 25, 50, 300);
    } else {
        // 150 psig +/- 10%,  Min 50 psig, Max 300 psig
        state.pressure = vary(150, 10, 50, 300);
    }

    return state;
}
```

<span data-ttu-id="bd38f-121">You can view the complete [chiller-01-state.js](https://github.com/Azure/device-simulation-dotnet/blob/master/Services/data/devicemodels/scripts/chiller-01-state.js) on Github.</span><span class="sxs-lookup"><span data-stu-id="bd38f-121">You can view the complete [chiller-01-state.js](https://github.com/Azure/device-simulation-dotnet/blob/master/Services/data/devicemodels/scripts/chiller-01-state.js) on Github.</span></span>

## <a name="method-behavior"></a><span data-ttu-id="bd38f-122">Method behavior</span><span class="sxs-lookup"><span data-stu-id="bd38f-122">Method behavior</span></span>

<span data-ttu-id="bd38f-123">The [CloudToDeviceMethods](../articles/iot-accelerators/iot-accelerators-device-simulation-device-schema.md#cloudtodevicemethods) section of the device model schema defines the methods a simulated device responds to.</span><span class="sxs-lookup"><span data-stu-id="bd38f-123">The [CloudToDeviceMethods](../articles/iot-accelerators/iot-accelerators-device-simulation-device-schema.md#cloudtodevicemethods) section of the device model schema defines the methods a simulated device responds to.</span></span>

<span data-ttu-id="bd38f-124">The following example shows the list of methods supported by a simulated chiller device:</span><span class="sxs-lookup"><span data-stu-id="bd38f-124">The following example shows the list of methods supported by a simulated chiller device:</span></span>

```json
"CloudToDeviceMethods": {
  "Reboot": {
    "Type": "javascript",
    "Path": "Reboot-method.js"
  },
  "FirmwareUpdate": {
    "Type": "javascript",
    "Path": "FirmwareUpdate-method.js"
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

<span data-ttu-id="bd38f-125">Each method has an associated JavaScript file that implements the behavior of the method.</span><span class="sxs-lookup"><span data-stu-id="bd38f-125">Each method has an associated JavaScript file that implements the behavior of the method.</span></span>

<span data-ttu-id="bd38f-126">The state of the simulated device, as defined in the `InitialState` section of the schema, is held in memory by the simulation service.</span><span class="sxs-lookup"><span data-stu-id="bd38f-126">The state of the simulated device, as defined in the `InitialState` section of the schema, is held in memory by the simulation service.</span></span> <span data-ttu-id="bd38f-127">The state information is passed as input to the `main` function defined in  the JavaScript file when the method is called.</span><span class="sxs-lookup"><span data-stu-id="bd38f-127">The state information is passed as input to the `main` function defined in  the JavaScript file when the method is called.</span></span> <span data-ttu-id="bd38f-128">The script can modify the state of the simulated device.</span><span class="sxs-lookup"><span data-stu-id="bd38f-128">The script can modify the state of the simulated device.</span></span>

<span data-ttu-id="bd38f-129">The following shows the outline of a typical `main` function:</span><span class="sxs-lookup"><span data-stu-id="bd38f-129">The following shows the outline of a typical `main` function:</span></span>

```javascript
function main(context, previousState, previousProperties) {

}
```

<span data-ttu-id="bd38f-130">The `context` parameter has the following properties:</span><span class="sxs-lookup"><span data-stu-id="bd38f-130">The `context` parameter has the following properties:</span></span>

- <span data-ttu-id="bd38f-131">`currentTime` as a string with format `yyyy-MM-dd'T'HH:mm:sszzz`</span><span class="sxs-lookup"><span data-stu-id="bd38f-131">`currentTime` as a string with format `yyyy-MM-dd'T'HH:mm:sszzz`</span></span>
- <span data-ttu-id="bd38f-132">`deviceId`, for example `Simulated.Chiller.123`</span><span class="sxs-lookup"><span data-stu-id="bd38f-132">`deviceId`, for example `Simulated.Chiller.123`</span></span>
- <span data-ttu-id="bd38f-133">`deviceModel`, for example `Chiller`</span><span class="sxs-lookup"><span data-stu-id="bd38f-133">`deviceModel`, for example `Chiller`</span></span>

<span data-ttu-id="bd38f-134">The `state` parameter contains the state of the device as maintained by the device simulation service.</span><span class="sxs-lookup"><span data-stu-id="bd38f-134">The `state` parameter contains the state of the device as maintained by the device simulation service.</span></span>

<span data-ttu-id="bd38f-135">The `properties` parameter contains the properties of the device that are written as reported properties to the IoT Hub device twin.</span><span class="sxs-lookup"><span data-stu-id="bd38f-135">The `properties` parameter contains the properties of the device that are written as reported properties to the IoT Hub device twin.</span></span>

<span data-ttu-id="bd38f-136">There are three global functions you can use to help implement the behavior of the method:</span><span class="sxs-lookup"><span data-stu-id="bd38f-136">There are three global functions you can use to help implement the behavior of the method:</span></span>

- <span data-ttu-id="bd38f-137">`updateState` to update the state held by the simulation service.</span><span class="sxs-lookup"><span data-stu-id="bd38f-137">`updateState` to update the state held by the simulation service.</span></span>
- <span data-ttu-id="bd38f-138">`updateProperty` to update a single device property.</span><span class="sxs-lookup"><span data-stu-id="bd38f-138">`updateProperty` to update a single device property.</span></span>
- <span data-ttu-id="bd38f-139">`sleep` to pause execution to simulate a long-running task.</span><span class="sxs-lookup"><span data-stu-id="bd38f-139">`sleep` to pause execution to simulate a long-running task.</span></span>

<span data-ttu-id="bd38f-140">The following example shows an abbreviated version of the **IncreasePressure-method.js** script used by the simulated chiller devices:</span><span class="sxs-lookup"><span data-stu-id="bd38f-140">The following example shows an abbreviated version of the **IncreasePressure-method.js** script used by the simulated chiller devices:</span></span>

```javascript
function main(context, previousState, previousProperties) {

    log("Starting 'Increase Pressure' method simulation (5 seconds)");

    // Pause the simulation and change the simulation mode so that the
    // temperature will fluctuate at ~250 when it resumes
    var state = {
        simulation_state: "high_pressure",
        CalculateRandomizedTelemetry: false
    };
    updateState(state);

    // Increase
    state.pressure = 210;
    updateState(state);
    log("Pressure increased to " + state.pressure);
    sleep(1000);

    // Increase
    state.pressure = 250;
    updateState(state);
    log("Pressure increased to " + state.pressure);
    sleep(1000);

    // Resume the simulation
    state.CalculateRandomizedTelemetry = true;
    updateState(state);

    log("'Increase Pressure' method simulation completed");
}
```

## <a name="debugging-script-files"></a><span data-ttu-id="bd38f-141">Debugging script files</span><span class="sxs-lookup"><span data-stu-id="bd38f-141">Debugging script files</span></span>

<span data-ttu-id="bd38f-142">It's not possible to attach a debugger to the Javascript interpreter used by the device simulation service to run state and method scripts.</span><span class="sxs-lookup"><span data-stu-id="bd38f-142">It's not possible to attach a debugger to the Javascript interpreter used by the device simulation service to run state and method scripts.</span></span> <span data-ttu-id="bd38f-143">However, you can log information in the service log.</span><span class="sxs-lookup"><span data-stu-id="bd38f-143">However, you can log information in the service log.</span></span> <span data-ttu-id="bd38f-144">The built-in `log()` function enables you to save information to track and debug function execution.</span><span class="sxs-lookup"><span data-stu-id="bd38f-144">The built-in `log()` function enables you to save information to track and debug function execution.</span></span>

<span data-ttu-id="bd38f-145">If there is a syntax error the interpreter fails, and writes a `Jint.Runtime.JavaScriptException` entry to the service log.</span><span class="sxs-lookup"><span data-stu-id="bd38f-145">If there is a syntax error the interpreter fails, and writes a `Jint.Runtime.JavaScriptException` entry to the service log.</span></span>

<span data-ttu-id="bd38f-146">The [Running the service locally](https://github.com/Azure/device-simulation-dotnet#running-the-service-locally-eg-for-development-tasks) article on GitHub shows you how to run the device simulation service locally.</span><span class="sxs-lookup"><span data-stu-id="bd38f-146">The [Running the service locally](https://github.com/Azure/device-simulation-dotnet#running-the-service-locally-eg-for-development-tasks) article on GitHub shows you how to run the device simulation service locally.</span></span> <span data-ttu-id="bd38f-147">Running the service locally makes it easier to debug your simulated devices before you deploy them to the cloud.</span><span class="sxs-lookup"><span data-stu-id="bd38f-147">Running the service locally makes it easier to debug your simulated devices before you deploy them to the cloud.</span></span>