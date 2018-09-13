---
title: Get started with Azure IoT Hub module identity and module twin (Python) | Microsoft Docs
description: Learn how to create module identity and update module twin using IoT SDKs for Python.
author: chrissie926
manager: ''
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: menchi
ms.openlocfilehash: 5a4d9debfcc48279bbb56df076a77a5c8b44e231
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867061"
---
# <a name="get-started-with-iot-hub-module-identity-and-module-twin-using-python-back-end-and-python-device"></a><span data-ttu-id="37834-103">Get started with IoT Hub module identity and module twin using Python back end and Python device</span><span class="sxs-lookup"><span data-stu-id="37834-103">Get started with IoT Hub module identity and module twin using Python back end and Python device</span></span>

> [!NOTE]
> <span data-ttu-id="37834-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span><span class="sxs-lookup"><span data-stu-id="37834-104">[Module identities and module twins](iot-hub-devguide-module-twins.md) are similar to Azure IoT Hub device identity and device twin, but provide finer granularity.</span></span> <span data-ttu-id="37834-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span><span class="sxs-lookup"><span data-stu-id="37834-105">While Azure IoT Hub device identity and device twin enable the back-end application to configure a device and provides visibility on the device’s conditions, a module identity and module twin provide these capabilities for individual components of a device.</span></span> <span data-ttu-id="37834-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span><span class="sxs-lookup"><span data-stu-id="37834-106">On capable devices with multiple components, such as operating system based devices or firmware devices, it allows for isolated configuration and conditions for each component.</span></span>

<span data-ttu-id="37834-107">At the end of this tutorial, you have two Python apps:</span><span class="sxs-lookup"><span data-stu-id="37834-107">At the end of this tutorial, you have two Python apps:</span></span>

* <span data-ttu-id="37834-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span><span class="sxs-lookup"><span data-stu-id="37834-108">**CreateIdentities**, which creates a device identity, a module identity and associated security key to connect your device and module clients.</span></span>
* <span data-ttu-id="37834-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="37834-109">**UpdateModuleTwinReportedProperties**, which sends updated module twin reported properties to your IoT Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="37834-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="37834-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="37834-111">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="37834-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="37834-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="37834-112">An active Azure account.</span></span> <span data-ttu-id="37834-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="37834-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>
* <span data-ttu-id="37834-114">An IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="37834-114">An IoT Hub.</span></span>
* <span data-ttu-id="37834-115">Install the latest [Python SDK](https://github.com/Azure/azure-iot-sdk-python).</span><span class="sxs-lookup"><span data-stu-id="37834-115">Install the latest [Python SDK](https://github.com/Azure/azure-iot-sdk-python).</span></span>


<span data-ttu-id="37834-116">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="37834-116">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity-and-a-module-identity-in-iot-hub"></a><span data-ttu-id="37834-117">Create a device identity and a module identity in IoT Hub</span><span class="sxs-lookup"><span data-stu-id="37834-117">Create a device identity and a module identity in IoT Hub</span></span>

<span data-ttu-id="37834-118">In this section, you create a Python app that creates a device identity and a module identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="37834-118">In this section, you create a Python app that creates a device identity and a module identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="37834-119">A device or module cannot connect to IoT hub unless it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="37834-119">A device or module cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="37834-120">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="37834-120">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="37834-121">When you run this console app, it generates a unique ID and key for both device and module.</span><span class="sxs-lookup"><span data-stu-id="37834-121">When you run this console app, it generates a unique ID and key for both device and module.</span></span> <span data-ttu-id="37834-122">Your device and module use these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="37834-122">Your device and module use these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="37834-123">The IDs are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="37834-123">The IDs are case-sensitive.</span></span>

<span data-ttu-id="37834-124">Add the following code to your Python file:</span><span class="sxs-lookup"><span data-stu-id="37834-124">Add the following code to your Python file:</span></span>

```Python
import sys
import iothub_service_client
from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod, IoTHubError

CONNECTION_STRING = "YourConnString"
DEVICE_ID = "myFirstDevice"
MODULE_ID = "myFirstModule"

try:
    # RegistryManager
    iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)

    # CreateDevice
    primary_key = ""
    secondary_key = ""
    auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
    new_device = iothub_registry_manager.create_device(DEVICE_ID, primary_key, secondary_key, auth_method)
    print("new_device <" + DEVICE_ID + "> has primary key = " + new_device.primaryKey)

    # CreateModule
    new_module = iothub_registry_manager.create_module(DEVICE_ID, primary_key, secondary_key, MODULE_ID, auth_method)
    print("device/new_module <" + DEVICE_ID + "/" + MODULE_ID + "> has primary key = " + new_module.primaryKey)

except IoTHubError as iothub_error:
    print ( "Unexpected error {0}".format(iothub_error) )
except KeyboardInterrupt:
    print ( "IoTHubRegistryManager sample stopped" )
```

<span data-ttu-id="37834-125">This app creates a device identity with ID **myFirstDevice** and a module identity with ID **myFirstModule** under device **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="37834-125">This app creates a device identity with ID **myFirstDevice** and a module identity with ID **myFirstModule** under device **myFirstDevice**.</span></span> <span data-ttu-id="37834-126">(If that module ID already exists in the identity registry, the code simply retrieves the existing module information.) The app then displays the primary key for that identity.</span><span class="sxs-lookup"><span data-stu-id="37834-126">(If that module ID already exists in the identity registry, the code simply retrieves the existing module information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="37834-127">You use this key in the simulated module app to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="37834-127">You use this key in the simulated module app to connect to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="37834-128">The IoT Hub identity registry only stores device and module identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="37834-128">The IoT Hub identity registry only stores device and module identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="37834-129">The identity registry stores device IDs and keys to use as security credentials.</span><span class="sxs-lookup"><span data-stu-id="37834-129">The identity registry stores device IDs and keys to use as security credentials.</span></span> <span data-ttu-id="37834-130">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span><span class="sxs-lookup"><span data-stu-id="37834-130">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span></span> <span data-ttu-id="37834-131">If your application needs to store other device-specific metadata, it should use an application-specific store.</span><span class="sxs-lookup"><span data-stu-id="37834-131">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="37834-132">There is no enabled/disabled flag for module identities.</span><span class="sxs-lookup"><span data-stu-id="37834-132">There is no enabled/disabled flag for module identities.</span></span> <span data-ttu-id="37834-133">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="37834-133">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="update-the-module-twin-using-python-device-sdk"></a><span data-ttu-id="37834-134">Update the module twin using Python device SDK</span><span class="sxs-lookup"><span data-stu-id="37834-134">Update the module twin using Python device SDK</span></span>

<span data-ttu-id="37834-135">In this section, you create a Python app on your simulated device that updates the module twin reported properties.</span><span class="sxs-lookup"><span data-stu-id="37834-135">In this section, you create a Python app on your simulated device that updates the module twin reported properties.</span></span>

1. <span data-ttu-id="37834-136">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="37834-136">**Get your module connection string** -- now if you login to [Azure portal][lnk-portal].</span></span> <span data-ttu-id="37834-137">Navigate to your IoT Hub and click IoT Devices.</span><span class="sxs-lookup"><span data-stu-id="37834-137">Navigate to your IoT Hub and click IoT Devices.</span></span> <span data-ttu-id="37834-138">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span><span class="sxs-lookup"><span data-stu-id="37834-138">Find myFirstDevice, open it and you see myFirstModule was successfuly created.</span></span> <span data-ttu-id="37834-139">Copy the module connection string.</span><span class="sxs-lookup"><span data-stu-id="37834-139">Copy the module connection string.</span></span> <span data-ttu-id="37834-140">It is needed in the next step.</span><span class="sxs-lookup"><span data-stu-id="37834-140">It is needed in the next step.</span></span>

    ![Azure portal module detail][15]

2. <span data-ttu-id="37834-142">**Create UpdateModuleTwinReportedProperties app** Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="37834-142">**Create UpdateModuleTwinReportedProperties app** Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```Python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod, IoTHubDeviceTwin, IoTHubError

    CONNECTION_STRING = "FILL IN CONNECTION STRING"
    DEVICE_ID = "MyFirstDevice"
    MODULE_ID = "MyFirstModule"

    UPDATE_JSON = "{\"properties\":{\"desired\":{\"telemetryInterval\":122}}}"

    try:
        iothub_twin = IoTHubDeviceTwin(CONNECTION_STRING)

        twin_info = iothub_twin.get_twin(DEVICE_ID, MODULE_ID)
        print ( "" )
        print ( "Twin before update    :" )
        print ( "{0}".format(twin_info) )

        twin_info_updated = iothub_twin.update_twin(DEVICE_ID, MODULE_ID, UPDATE_JSON)
        print ( "" )
        print ( "Twin after update     :" )
        print ( "{0}".format(twin_info_updated) )

    except IoTHubError as iothub_error:
        print ( "Unexpected error {0}".format(iothub_error) )
    except KeyboardInterrupt:
        print ( "IoTHubRegistryManager sample stopped" )
    ```

<span data-ttu-id="37834-143">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="37834-143">This code sample shows you how to retrieve the module twin and update reported properties with AMQP protocol.</span></span> 

## <a name="get-updates-on-the-device-side"></a><span data-ttu-id="37834-144">Get updates on the device side</span><span class="sxs-lookup"><span data-stu-id="37834-144">Get updates on the device side</span></span>
<span data-ttu-id="37834-145">In addition to the above code, you can add below code block to get the twin update message on your device.</span><span class="sxs-lookup"><span data-stu-id="37834-145">In addition to the above code, you can add below code block to get the twin update message on your device.</span></span>

```Python
import random
import time
import sys
import iothub_client
from iothub_client import IoTHubModuleClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult

PROTOCOL = IoTHubTransportProvider.AMQP
CONNECTION_STRING = ""

def module_twin_callback(update_state, payload, user_context):
    print ("")
    print ("Twin callback called with:")
    print ("updateStatus: %s" % update_state )
    print ("context: %s" % user_context )
    print ("payload: %s" % payload )

try:
    module_client = IoTHubModuleClient(CONNECTION_STRING, PROTOCOL)
    module_client.set_module_twin_callback(module_twin_callback, 1234)

    print ("Waiting for incoming twin messages.  Hit Control-C to exit.")
    while True:

        time.sleep(1000000)

except IoTHubError as iothub_error:
    print ( "Unexpected error {0}".format(iothub_error) )
except KeyboardInterrupt:
    print ( "module client sample stopped" )
```


## <a name="next-steps"></a><span data-ttu-id="37834-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="37834-146">Next steps</span></span>

<span data-ttu-id="37834-147">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="37834-147">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="37834-148">[Getting started with device management][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="37834-148">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="37834-149">[Getting started with IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="37834-149">[Getting started with IoT Edge][lnk-iot-edge]</span></span>


<!-- Images. -->
[15]: ./media\iot-hub-csharp-csharp-module-twin-getstarted/module-detail.JPG
<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/