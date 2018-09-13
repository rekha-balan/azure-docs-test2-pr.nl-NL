---
title: Schedule jobs with Azure IoT Hub (Python) | Microsoft Docs
description: How to schedule an Azure IoT Hub job to invoke a direct method on multiple devices. You use the Azure IoT SDKs for Python to implement the simulated device apps and a service app to run the job.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 02/16/2018
ms.author: kgremban
ms.openlocfilehash: 588ee4b7d728aa16201cbe9c325d25a9cc5c9884
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855652"
---
# <a name="schedule-and-broadcast-jobs-python"></a><span data-ttu-id="6eeeb-104">Schedule and broadcast jobs (Python)</span><span class="sxs-lookup"><span data-stu-id="6eeeb-104">Schedule and broadcast jobs (Python)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="6eeeb-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="6eeeb-106">Jobs can be used for the following actions:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="6eeeb-107">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="6eeeb-107">Update desired properties</span></span>
* <span data-ttu-id="6eeeb-108">Update tags</span><span class="sxs-lookup"><span data-stu-id="6eeeb-108">Update tags</span></span>
* <span data-ttu-id="6eeeb-109">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="6eeeb-109">Invoke direct methods</span></span>

<span data-ttu-id="6eeeb-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="6eeeb-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="6eeeb-112">That application can then track progress as each of those devices receive and execute the reboot method.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="6eeeb-113">Learn more about each of these capabilities in these articles:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="6eeeb-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="6eeeb-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="6eeeb-115">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="6eeeb-115">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="6eeeb-116">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6eeeb-117">Create a Python simulated device app that has a direct method, which enables **lockDoor**, which can be called by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-117">Create a Python simulated device app that has a direct method, which enables **lockDoor**, which can be called by the solution back end.</span></span>
* <span data-ttu-id="6eeeb-118">Create a Python console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-118">Create a Python console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="6eeeb-119">At the end of this tutorial, you have two Python apps:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-119">At the end of this tutorial, you have two Python apps:</span></span>

<span data-ttu-id="6eeeb-120">**simDevice.py**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-120">**simDevice.py**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="6eeeb-121">**scheduleJobService.py**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-121">**scheduleJobService.py**, which calls a direct method in the simulated device app and updates the device twin's desired properties using a job.</span></span>

<span data-ttu-id="6eeeb-122">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6eeeb-123">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="6eeeb-123">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="6eeeb-124">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-124">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="6eeeb-125">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-125">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="6eeeb-126">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="6eeeb-126">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="6eeeb-127">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-127">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="6eeeb-128">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-128">An active Azure account.</span></span> <span data-ttu-id="6eeeb-129">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="6eeeb-129">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

> [!NOTE]
> <span data-ttu-id="6eeeb-130">The **Azure IoT SDK for Python** does not directly support **Jobs** functionality.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-130">The **Azure IoT SDK for Python** does not directly support **Jobs** functionality.</span></span> <span data-ttu-id="6eeeb-131">Instead this tutorial offers an alternate solution utilizing asynchronous threads and timers.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-131">Instead this tutorial offers an alternate solution utilizing asynchronous threads and timers.</span></span> <span data-ttu-id="6eeeb-132">For further updates, see the **Service Client SDK** feature list on the [Azure IoT SDK for Python](https://github.com/Azure/azure-iot-sdk-python) page.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-132">For further updates, see the **Service Client SDK** feature list on the [Azure IoT SDK for Python](https://github.com/Azure/azure-iot-sdk-python) page.</span></span> 
> 
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6eeeb-133">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="6eeeb-133">Create a simulated device app</span></span>
<span data-ttu-id="6eeeb-134">In this section, you create a Python console app that responds to a direct method called by the cloud, which triggers a simulated **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-134">In this section, you create a Python console app that responds to a direct method called by the cloud, which triggers a simulated **lockDoor** method.</span></span>

1. <span data-ttu-id="6eeeb-135">At your command prompt, run the following command to install the **azure-iot-device-client** package:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-135">At your command prompt, run the following command to install the **azure-iot-device-client** package:</span></span>
   
    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. <span data-ttu-id="6eeeb-136">Using a text editor, create a new **simDevice.py** file in your working directory.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-136">Using a text editor, create a new **simDevice.py** file in your working directory.</span></span>

1. <span data-ttu-id="6eeeb-137">Add the following `import` statements and variables at the start of the **simDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-137">Add the following `import` statements and variables at the start of the **simDevice.py** file.</span></span> <span data-ttu-id="6eeeb-138">Replace `deviceConnectionString` with the connection string of the device you created above:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-138">Replace `deviceConnectionString` with the connection string of the device you created above:</span></span>
   
    ```python
    import time
    import sys

    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubError, DeviceMethodReturnValue

    METHOD_CONTEXT = 0
    TWIN_CONTEXT = 0
    WAIT_COUNT = 10

    PROTOCOL = IoTHubTransportProvider.MQTT
    CONNECTION_STRING = "{deviceConnectionString}"
    ```

1. <span data-ttu-id="6eeeb-139">Add the following function callback to handle the **lockDoor** method:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-139">Add the following function callback to handle the **lockDoor** method:</span></span>
   
    ```python
    def device_method_callback(method_name, payload, user_context):
        if method_name == "lockDoor":
            print ( "Locking Door!" )

            device_method_return_value = DeviceMethodReturnValue()
            device_method_return_value.response = "{ \"Response\": \"lockDoor called successfully\" }"
            device_method_return_value.status = 200
            return device_method_return_value
    ```

1. <span data-ttu-id="6eeeb-140">Add another function callback to handle device twins updates:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-140">Add another function callback to handle device twins updates:</span></span>

    ```python
    def device_twin_callback(update_state, payload, user_context):
        print ( "")
        print ( "Twin callback called with:")
        print ( "payload: %s" % payload )
    ```

1. <span data-ttu-id="6eeeb-141">Add the following code to register the handler for the **lockDoor** method.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-141">Add the following code to register the handler for the **lockDoor** method.</span></span> <span data-ttu-id="6eeeb-142">Also include the `main` routine:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-142">Also include the `main` routine:</span></span>
   
    ```python
    def iothub_jobs_sample_run():
        try:
            client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
            client.set_device_method_callback(device_method_callback, METHOD_CONTEXT)
            client.set_device_twin_callback(device_twin_callback, TWIN_CONTEXT)

            print ( "Direct method initialized." )
            print ( "Device twin callback initialized." )
            print ( "IoTHubClient waiting for commands, press Ctrl-C to exit" )
        
            while True:
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
        print ( "Starting the IoT Hub Python jobs sample..." )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_jobs_sample_run()
    ```

1. <span data-ttu-id="6eeeb-143">Save and close the **simDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-143">Save and close the **simDevice.py** file.</span></span>

> [!NOTE]
> <span data-ttu-id="6eeeb-144">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-144">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6eeeb-145">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="6eeeb-145">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 


## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="6eeeb-146">Schedule jobs for calling a direct method and updating a device twin's properties</span><span class="sxs-lookup"><span data-stu-id="6eeeb-146">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="6eeeb-147">In this section, you create a Python console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-147">In this section, you create a Python console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="6eeeb-148">At your command prompt, run the following command to install the **azure-iot-service-client** package:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-148">At your command prompt, run the following command to install the **azure-iot-service-client** package:</span></span>
   
    ```cmd/sh
    pip install azure-iothub-service-client
    ```

1. <span data-ttu-id="6eeeb-149">Using a text editor, create a new **scheduleJobService.py** file in your working directory.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-149">Using a text editor, create a new **scheduleJobService.py** file in your working directory.</span></span>

1. <span data-ttu-id="6eeeb-150">Add the following `import` statements and variables at the start of the **scheduleJobService.py** file:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-150">Add the following `import` statements and variables at the start of the **scheduleJobService.py** file:</span></span>
   
    ```python
    import sys
    import time
    import threading
    import uuid

    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceTwin, IoTHubDeviceMethod, IoTHubError

    CONNECTION_STRING = "{IoTHubConnectionString}"
    DEVICE_ID = "{deviceId}"

    METHOD_NAME = "lockDoor"
    METHOD_PAYLOAD = "{\"lockTime\":\"10m\"}"
    UPDATE_JSON = "{\"properties\":{\"desired\":{\"building\":43,\"floor\":3}}}"
    TIMEOUT = 60
    WAIT_COUNT = 5
    ```

1. <span data-ttu-id="6eeeb-151">Add the following function that is used to query for devices:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-151">Add the following function that is used to query for devices:</span></span>
   
    ```python
    def query_condition(device_id):
        iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
    
        number_of_devices = 10
        dev_list = iothub_registry_manager.get_device_list(number_of_devices)
    
        for device in range(0, number_of_devices):
            if dev_list[device].deviceId == device_id:
                return 1

        print ( "Device not found" )
        return 0
    ```

1. <span data-ttu-id="6eeeb-152">Add the following methods to run the jobs that call the direct method and device twin:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-152">Add the following methods to run the jobs that call the direct method and device twin:</span></span>
   
    ```python
    def device_method_job(job_id, device_id, wait_time, execution_time):
        print ( "" )
        print ( "Scheduling job: " + str(job_id) )
        time.sleep(wait_time)
    
        if query_condition(device_id):
            iothub_device_method = IoTHubDeviceMethod(CONNECTION_STRING)
    
            response = iothub_device_method.invoke(device_id, METHOD_NAME, METHOD_PAYLOAD, TIMEOUT)
        
            print ( "" )
            print ( "Direct method " + METHOD_NAME + " called." )
        
    def device_twin_job(job_id, device_id, wait_time, execution_time):
        print ( "" )
        print ( "Scheduling job " + str(job_id) )
        time.sleep(wait_time)
    
        if query_condition(device_id):
            iothub_twin_method = IoTHubDeviceTwin(CONNECTION_STRING)
    
            twin_info = iothub_twin_method.update_twin(DEVICE_ID, UPDATE_JSON)
        
            print ( "" )
            print ( "Device twin updated." )
    ```

1. <span data-ttu-id="6eeeb-153">Add the following code to schedule the jobs and update job status.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-153">Add the following code to schedule the jobs and update job status.</span></span> <span data-ttu-id="6eeeb-154">Also include the `main` routine:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-154">Also include the `main` routine:</span></span>
   
    ```python
    def iothub_jobs_sample_run():
        try:
            method_thr_id = uuid.uuid4()
            method_thr = threading.Thread(target=device_method_job, args=(method_thr_id, DEVICE_ID, 20, TIMEOUT), kwargs={})
            method_thr.start()
        
            print ( "" )
            print ( "Direct method called with Job Id: " + str(method_thr_id) )
        
            twin_thr_id = uuid.uuid4()
            twin_thr = threading.Thread(target=device_twin_job, args=(twin_thr_id, DEVICE_ID, 10, TIMEOUT), kwargs={})
            twin_thr.start()
        
            print ( "" )
            print ( "Device twin called with Job Id: " + str(twin_thr_id) )
        
            while True:
                print ( "" )
            
                if method_thr.is_alive():
                    print ( "...job " + str(method_thr_id) + " still running." )
                else:
                    print ( "...job " + str(method_thr_id) + " complete." )
            
                if twin_thr.is_alive():
                    print ( "...job " + str(twin_thr_id) + " still running." )
                else:
                    print ( "...job " + str(twin_thr_id) + " complete." )
                
                print ( "Job status posted, press Ctrl-C to exit" )

                status_counter = 0
                while status_counter <= WAIT_COUNT:
                    time.sleep(1)
                    status_counter += 1

        except IoTHubError as iothub_error:
            print ( "" )
            print ( "Unexpected error {0}" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "" )
            print ( "IoTHubService sample stopped" )

    if __name__ == '__main__':
        print ( "Starting the IoT Hub jobs Python sample..." )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_jobs_sample_run()
    ```

1. <span data-ttu-id="6eeeb-155">Save and close the **scheduleJobService.py** file.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-155">Save and close the **scheduleJobService.py** file.</span></span>


## <a name="run-the-applications"></a><span data-ttu-id="6eeeb-156">Run the applications</span><span class="sxs-lookup"><span data-stu-id="6eeeb-156">Run the applications</span></span>
<span data-ttu-id="6eeeb-157">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-157">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="6eeeb-158">At the command prompt in your working directory, run the following command to begin listening for the reboot direct method:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-158">At the command prompt in your working directory, run the following command to begin listening for the reboot direct method:</span></span>
   
    ```cmd/sh
    python simDevice.py
    ```

1. <span data-ttu-id="6eeeb-159">At another command prompt in your working directory, run the following command to trigger the jobs to lock the door and update the twin:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-159">At another command prompt in your working directory, run the following command to trigger the jobs to lock the door and update the twin:</span></span>
   
    ```cmd/sh
    python scheduleJobService.py
    ```

1. <span data-ttu-id="6eeeb-160">You see the device responses to the direct method and device twins update in the console.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-160">You see the device responses to the direct method and device twins update in the console.</span></span>

    ![device output][1]

    ![service output][2]


## <a name="next-steps"></a><span data-ttu-id="6eeeb-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="6eeeb-163">Next steps</span></span>
<span data-ttu-id="6eeeb-164">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span><span class="sxs-lookup"><span data-stu-id="6eeeb-164">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="6eeeb-165">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span><span class="sxs-lookup"><span data-stu-id="6eeeb-165">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="6eeeb-166">[Tutorial: How to do a firmware update][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="6eeeb-166">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="6eeeb-167">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="6eeeb-167">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-python-twin-getstarted.md
[lnk-twin-props]: tutorial-device-twins.md
[lnk-c2d-methods]: quickstart-control-device-python.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: tutorial-firmware-update.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-transient-faults]: https://docs.microsoft.com/azure/architecture/best-practices/transient-faults

[1]: ./media/iot-hub-python-python-schedule-jobs/1.png
[2]: ./media/iot-hub-python-python-schedule-jobs/2.png
