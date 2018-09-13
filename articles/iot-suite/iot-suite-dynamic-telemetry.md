---
title: Use dynamic telemetry | Microsoft Docs
description: Follow this tutorial to learn how to use dynamic telemetry with the Azure IoT Suite remote monitoring preconfigured solution.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/09/2017
ms.author: dobett
ms.openlocfilehash: 32f4f1bb2030881509f44b79e5f776fc27b476da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549638"
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="a4b16-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="a4b16-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>
## <a name="introduction"></a><span data-ttu-id="a4b16-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="a4b16-104">Introduction</span></span>
<span data-ttu-id="a4b16-105">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="a4b16-105">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a4b16-106">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b16-106">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="a4b16-107">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span><span class="sxs-lookup"><span data-stu-id="a4b16-107">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="a4b16-108">You can then visualize this additional telemetry on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b16-108">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="a4b16-109">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span><span class="sxs-lookup"><span data-stu-id="a4b16-109">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="a4b16-110">To complete this tutorial, you’ll need:</span><span class="sxs-lookup"><span data-stu-id="a4b16-110">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="a4b16-111">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a4b16-111">An active Azure subscription.</span></span> <span data-ttu-id="a4b16-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="a4b16-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a4b16-113">For details, see [Azure Free Trial][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="a4b16-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="a4b16-114">[Node.js][lnk-node] version 0.12.x or later.</span><span class="sxs-lookup"><span data-stu-id="a4b16-114">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="a4b16-115">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span><span class="sxs-lookup"><span data-stu-id="a4b16-115">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="a4b16-116">Add a telemetry type</span><span class="sxs-lookup"><span data-stu-id="a4b16-116">Add a telemetry type</span></span>
<span data-ttu-id="a4b16-117">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span><span class="sxs-lookup"><span data-stu-id="a4b16-117">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="a4b16-118">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span><span class="sxs-lookup"><span data-stu-id="a4b16-118">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="a4b16-119">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span><span class="sxs-lookup"><span data-stu-id="a4b16-119">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="a4b16-120">Add a base data value for **rpm** as follows:</span><span class="sxs-lookup"><span data-stu-id="a4b16-120">Add a base data value for **rpm** as follows:</span></span>
   
    ```
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```
3. <span data-ttu-id="a4b16-121">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span><span class="sxs-lookup"><span data-stu-id="a4b16-121">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="a4b16-122">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span><span class="sxs-lookup"><span data-stu-id="a4b16-122">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>
   
    ```
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```
4. <span data-ttu-id="a4b16-123">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="a4b16-123">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>
   
    ```
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```
5. <span data-ttu-id="a4b16-124">Run the Node.js simulated device using the following command:</span><span class="sxs-lookup"><span data-stu-id="a4b16-124">Run the Node.js simulated device using the following command:</span></span>
   
    ```
    node remote_monitoring.js
    ```
6. <span data-ttu-id="a4b16-125">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span><span class="sxs-lookup"><span data-stu-id="a4b16-125">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![Add RPM to the dashboard][image3]

> [!NOTE]
> <span data-ttu-id="a4b16-127">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span><span class="sxs-lookup"><span data-stu-id="a4b16-127">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>
> 
> 

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="a4b16-128">Customize the dashboard display</span><span class="sxs-lookup"><span data-stu-id="a4b16-128">Customize the dashboard display</span></span>
<span data-ttu-id="a4b16-129">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a4b16-129">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="a4b16-130">This metadata can specify the telemetry types the device sends.</span><span class="sxs-lookup"><span data-stu-id="a4b16-130">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="a4b16-131">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span><span class="sxs-lookup"><span data-stu-id="a4b16-131">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="a4b16-132">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span><span class="sxs-lookup"><span data-stu-id="a4b16-132">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

```
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="a4b16-133">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span><span class="sxs-lookup"><span data-stu-id="a4b16-133">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>
> 
> 

<span data-ttu-id="a4b16-134">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b16-134">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="a4b16-135">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a4b16-135">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="a4b16-136">Update the **Telemetry** metadata definition as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="a4b16-136">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

```
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="a4b16-137">The following screenshot shows how this change modifies the chart legend on the dashboard:</span><span class="sxs-lookup"><span data-stu-id="a4b16-137">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Customize the chart legend][image4]

> [!NOTE]
> <span data-ttu-id="a4b16-139">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span><span class="sxs-lookup"><span data-stu-id="a4b16-139">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>
> 
> 

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="a4b16-140">Filter the telemetry types</span><span class="sxs-lookup"><span data-stu-id="a4b16-140">Filter the telemetry types</span></span>
<span data-ttu-id="a4b16-141">By default, the chart on the dashboard shows every data series in the telemetry stream.</span><span class="sxs-lookup"><span data-stu-id="a4b16-141">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="a4b16-142">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span><span class="sxs-lookup"><span data-stu-id="a4b16-142">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="a4b16-143">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span><span class="sxs-lookup"><span data-stu-id="a4b16-143">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

```
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="a4b16-144">The **Outdoor Temperature** no longer displays on the chart:</span><span class="sxs-lookup"><span data-stu-id="a4b16-144">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Filter the telemetry on the dashboard][image5]

<span data-ttu-id="a4b16-146">This change only affects the chart display.</span><span class="sxs-lookup"><span data-stu-id="a4b16-146">This change only affects the chart display.</span></span> <span data-ttu-id="a4b16-147">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span><span class="sxs-lookup"><span data-stu-id="a4b16-147">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="a4b16-148">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span><span class="sxs-lookup"><span data-stu-id="a4b16-148">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>
> 
> 

## <a name="handle-errors"></a><span data-ttu-id="a4b16-149">Handle errors</span><span class="sxs-lookup"><span data-stu-id="a4b16-149">Handle errors</span></span>
<span data-ttu-id="a4b16-150">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span><span class="sxs-lookup"><span data-stu-id="a4b16-150">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="a4b16-151">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span><span class="sxs-lookup"><span data-stu-id="a4b16-151">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="a4b16-152">However, the **Humidity** values are still stored and made available for any backend processing.</span><span class="sxs-lookup"><span data-stu-id="a4b16-152">However, the **Humidity** values are still stored and made available for any backend processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4b16-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4b16-153">Next steps</span></span>
<span data-ttu-id="a4b16-154">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="a4b16-154">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-dynamic-telemetry/image3.png
[image4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-dynamic-telemetry/image4.png
[image5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org


