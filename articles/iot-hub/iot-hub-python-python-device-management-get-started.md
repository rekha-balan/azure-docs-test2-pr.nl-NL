---
title: Get started with Azure IoT Hub device management (Python) | Microsoft Docs
description: How to use IoT Hub device management to initiate a remote device reboot. You use the Azure IoT SDK for Python to implement a simulated device app that includes a direct method and a service app that invokes the direct method.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 01/02/2018
ms.author: kgremban
ms.openlocfilehash: fa966ee2ea26cccc7d841a0e969d8329ac5bc0de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856139"
---
# <a name="get-started-with-device-management-python"></a><span data-ttu-id="e4f99-104">Get started with device management (Python)</span><span class="sxs-lookup"><span data-stu-id="e4f99-104">Get started with device management (Python)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="e4f99-105">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="e4f99-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="e4f99-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e4f99-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="e4f99-107">Create a simulated device app that contains a direct method that reboots that device.</span><span class="sxs-lookup"><span data-stu-id="e4f99-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="e4f99-108">Direct methods are invoked from the cloud.</span><span class="sxs-lookup"><span data-stu-id="e4f99-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="e4f99-109">Create a Python console app that calls the reboot direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e4f99-109">Create a Python console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="e4f99-110">At the end of this tutorial, you have two Python console apps:</span><span class="sxs-lookup"><span data-stu-id="e4f99-110">At the end of this tutorial, you have two Python console apps:</span></span>

<span data-ttu-id="e4f99-111">**dmpatterns_getstarted_device.py**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span><span class="sxs-lookup"><span data-stu-id="e4f99-111">**dmpatterns_getstarted_device.py**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="e4f99-112">**dmpatterns_getstarted_service.py**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="e4f99-112">**dmpatterns_getstarted_service.py**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="e4f99-113">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="e4f99-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e4f99-114">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="e4f99-114">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="e4f99-115">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="e4f99-115">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="e4f99-116">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span><span class="sxs-lookup"><span data-stu-id="e4f99-116">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="e4f99-117">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="e4f99-117">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
    * <span data-ttu-id="e4f99-118">Install the [azure-iothub-device-client](https://pypi.org/project/azure-iothub-device-client/) package, using the command   `pip install azure-iothub-device-client`</span><span class="sxs-lookup"><span data-stu-id="e4f99-118">Install the [azure-iothub-device-client](https://pypi.org/project/azure-iothub-device-client/) package, using the command   `pip install azure-iothub-device-client`</span></span>
    * <span data-ttu-id="e4f99-119">Install the [azure-iothub-service-client](https://pypi.org/project/azure-iothub-service-client/) package, using the command   `pip install azure-iothub-service-client`</span><span class="sxs-lookup"><span data-stu-id="e4f99-119">Install the [azure-iothub-service-client](https://pypi.org/project/azure-iothub-service-client/) package, using the command   `pip install azure-iothub-service-client`</span></span>
* <span data-ttu-id="e4f99-120">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="e4f99-120">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="e4f99-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="e4f99-121">An active Azure account.</span></span> <span data-ttu-id="e4f99-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="e4f99-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e4f99-123">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="e4f99-123">Create a simulated device app</span></span>
<span data-ttu-id="e4f99-124">In this section, you will:</span><span class="sxs-lookup"><span data-stu-id="e4f99-124">In this section, you will:</span></span>

* <span data-ttu-id="e4f99-125">Create a Python console app that responds to a direct method called by the cloud</span><span class="sxs-lookup"><span data-stu-id="e4f99-125">Create a Python console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="e4f99-126">Simulate a device reboot</span><span class="sxs-lookup"><span data-stu-id="e4f99-126">Simulate a device reboot</span></span>
* <span data-ttu-id="e4f99-127">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span><span class="sxs-lookup"><span data-stu-id="e4f99-127">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="e4f99-128">Using a text editor, create a **dmpatterns_getstarted_device.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-128">Using a text editor, create a **dmpatterns_getstarted_device.py** file.</span></span>

1. <span data-ttu-id="e4f99-129">Add the following `import` statements at the start of the **dmpatterns_getstarted_device.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-129">Add the following `import` statements at the start of the **dmpatterns_getstarted_device.py** file.</span></span>
   
    ```python
    import random
    import time, datetime
    import sys

    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult, IoTHubError, DeviceMethodReturnValue
    ```

1. <span data-ttu-id="e4f99-130">Add variables including a **CONNECTION_STRING** variable and the client intialization.</span><span class="sxs-lookup"><span data-stu-id="e4f99-130">Add variables including a **CONNECTION_STRING** variable and the client intialization.</span></span>  <span data-ttu-id="e4f99-131">Replace the connection string with your device connection string.</span><span class="sxs-lookup"><span data-stu-id="e4f99-131">Replace the connection string with your device connection string.</span></span>  
   
    ```python
    CONNECTION_STRING = "{deviceConnectionString}"
    PROTOCOL = IoTHubTransportProvider.MQTT

    CLIENT = IoTHubClient(CONNECTION_STRING, PROTOCOL)

    WAIT_COUNT = 5

    SEND_REPORTED_STATE_CONTEXT = 0
    METHOD_CONTEXT = 0

    SEND_REPORTED_STATE_CALLBACKS = 0
    METHOD_CALLBACKS = 0
    ```

1. <span data-ttu-id="e4f99-132">Add the following function callbacks to implement the direct method on the device.</span><span class="sxs-lookup"><span data-stu-id="e4f99-132">Add the following function callbacks to implement the direct method on the device.</span></span>
   
    ```python
    def send_reported_state_callback(status_code, user_context):
        global SEND_REPORTED_STATE_CALLBACKS
    
        print ( "Device twins updated." )

    def device_method_callback(method_name, payload, user_context):
        global METHOD_CALLBACKS
    
        if method_name == "rebootDevice":
            print ( "Rebooting device..." )
        
            time.sleep(20)
        
            print ( "Device rebooted." )
        
            current_time = str(datetime.datetime.now())
            reported_state = "{\"rebootTime\":\"" + current_time + "\"}"
            CLIENT.send_reported_state(reported_state, len(reported_state), send_reported_state_callback, SEND_REPORTED_STATE_CONTEXT)
        
            print ( "Updating device twins: rebootTime" )
            
        device_method_return_value = DeviceMethodReturnValue()
        device_method_return_value.response = "{ \"Response\": \"This is the response from the device\" }"
        device_method_return_value.status = 200
    
        return device_method_return_value
    ```

1. <span data-ttu-id="e4f99-133">Start the direct method listener and wait.</span><span class="sxs-lookup"><span data-stu-id="e4f99-133">Start the direct method listener and wait.</span></span>
   
    ```python
    def iothub_client_init():
        if CLIENT.protocol == IoTHubTransportProvider.MQTT or client.protocol == IoTHubTransportProvider.MQTT_WS:
            CLIENT.set_device_method_callback(device_method_callback, METHOD_CONTEXT)
        
    def iothub_client_sample_run():
        try:
            iothub_client_init()

            while True:
                print ( "IoTHubClient waiting for commands, press Ctrl-C to exit" )

                status_counter = 0
                while status_counter <= WAIT_COUNT:
                    time.sleep(10)
                    status_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )

    if __name__ == '__main__':
        print ( "Starting the IoT Hub Python sample..." )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_sample_run()
    ```

1. <span data-ttu-id="e4f99-134">Save and close the **dmpatterns_getstarted_device.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-134">Save and close the **dmpatterns_getstarted_device.py** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e4f99-135">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="e4f99-135">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e4f99-136">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="e4f99-136">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="e4f99-137">Trigger a remote reboot on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="e4f99-137">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="e4f99-138">In this section, you create a Python console app that initiates a remote reboot on a device using a direct method.</span><span class="sxs-lookup"><span data-stu-id="e4f99-138">In this section, you create a Python console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="e4f99-139">The app uses device twin queries to discover the last reboot time for that device.</span><span class="sxs-lookup"><span data-stu-id="e4f99-139">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="e4f99-140">Using a text editor, create a **dmpatterns_getstarted_service.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-140">Using a text editor, create a **dmpatterns_getstarted_service.py** file.</span></span>

1. <span data-ttu-id="e4f99-141">Add the following `import` statements at the start of the **dmpatterns_getstarted_service.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-141">Add the following `import` statements at the start of the **dmpatterns_getstarted_service.py** file.</span></span>
   
    ```python
    import sys, time
    import iothub_service_client

    from iothub_service_client import IoTHubDeviceMethod, IoTHubError, IoTHubDeviceTwin
    ```

1. <span data-ttu-id="e4f99-142">Add the following variable declarations.</span><span class="sxs-lookup"><span data-stu-id="e4f99-142">Add the following variable declarations.</span></span> <span data-ttu-id="e4f99-143">Only replace placeholder values for _IoTHubConnectionString_ and _deviceId_.</span><span class="sxs-lookup"><span data-stu-id="e4f99-143">Only replace placeholder values for _IoTHubConnectionString_ and _deviceId_.</span></span>
   
    ```python
    CONNECTION_STRING = "{IoTHubConnectionString}"
    DEVICE_ID = "{deviceId}"

    METHOD_NAME = "rebootDevice"
    METHOD_PAYLOAD = "{\"method_number\":\"42\"}"
    TIMEOUT = 60
    WAIT_COUNT = 10
    ```

1. <span data-ttu-id="e4f99-144">Add the following function to invoke the device method to reboot the target device, then query for the device twins and get the last reboot time.</span><span class="sxs-lookup"><span data-stu-id="e4f99-144">Add the following function to invoke the device method to reboot the target device, then query for the device twins and get the last reboot time.</span></span>
   
    ```python
    def iothub_devicemethod_sample_run():
        try:
            iothub_twin_method = IoTHubDeviceTwin(CONNECTION_STRING)
            iothub_device_method = IoTHubDeviceMethod(CONNECTION_STRING)
        
            print ( "" )
            print ( "Invoking device to reboot..." )

            response = iothub_device_method.invoke(DEVICE_ID, METHOD_NAME, METHOD_PAYLOAD, TIMEOUT)

            print ( "" )
            print ( "Successfully invoked the device to reboot." )

            print ( "" )
            print ( response.payload )
        
            while True:
                print ( "" )
                print ( "IoTHubClient waiting for commands, press Ctrl-C to exit" )

                status_counter = 0
                while status_counter <= WAIT_COUNT:
                    twin_info = iothub_twin_method.get_twin(DEVICE_ID)
                
                    if twin_info.find("rebootTime") != -1:
                        print ( "Last reboot time: " + twin_info[twin_info.find("rebootTime")+11:twin_info.find("rebootTime")+37])
                    else:
                        print ("Waiting for device to report last reboot time...")

                    time.sleep(5)
                    status_counter += 1

        except IoTHubError as iothub_error:
            print ( "" )
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "" )
            print ( "IoTHubDeviceMethod sample stopped" )

    if __name__ == '__main__':
        print ( "Starting the IoT Hub Service Client DeviceManagement Python sample..." )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_devicemethod_sample_run()
    ```

1. <span data-ttu-id="e4f99-145">Save and close the **dmpatterns_getstarted_service.py** file.</span><span class="sxs-lookup"><span data-stu-id="e4f99-145">Save and close the **dmpatterns_getstarted_service.py** file.</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="e4f99-146">Run the apps</span><span class="sxs-lookup"><span data-stu-id="e4f99-146">Run the apps</span></span>
<span data-ttu-id="e4f99-147">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="e4f99-147">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="e4f99-148">At the command prompt, run the following command to begin listening for the reboot direct method.</span><span class="sxs-lookup"><span data-stu-id="e4f99-148">At the command prompt, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    python dmpatterns_getstarted_device.py
    ```

1. <span data-ttu-id="e4f99-149">At another command prompt, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span><span class="sxs-lookup"><span data-stu-id="e4f99-149">At another command prompt, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    python dmpatterns_getstarted_service.py
    ```

1. <span data-ttu-id="e4f99-150">You see the device response to the direct method in the console.</span><span class="sxs-lookup"><span data-stu-id="e4f99-150">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/

[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
