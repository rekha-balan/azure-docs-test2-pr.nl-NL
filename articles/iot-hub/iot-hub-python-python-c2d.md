---
title: Cloud-to-device messages with Azure IoT Hub (Python) | Microsoft Docs
description: How to send cloud-to-device messages to a device from an Azure IoT hub using the Azure IoT SDKs for Python. You modify a simulated device app to receive cloud-to-device messages and modify a back-end app to send the cloud-to-device messages.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: kgremban
ms.openlocfilehash: 316a8cd9ebf58e06ba39ba18fa19ede4b6a62229
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868772"
---
# <a name="send-cloud-to-device-messages-with-iot-hub-python"></a><span data-ttu-id="3a18e-104">Send cloud-to-device messages with IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="3a18e-104">Send cloud-to-device messages with IoT Hub (Python)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]


## <a name="introduction"></a><span data-ttu-id="3a18e-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="3a18e-105">Introduction</span></span>
<span data-ttu-id="3a18e-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="3a18e-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="3a18e-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="3a18e-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

<span data-ttu-id="3a18e-108">This tutorial builds on [Get started with IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="3a18e-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="3a18e-109">It shows you how to:</span><span class="sxs-lookup"><span data-stu-id="3a18e-109">It shows you how to:</span></span>

* <span data-ttu-id="3a18e-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a18e-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="3a18e-111">Receive cloud-to-device messages on a device.</span><span class="sxs-lookup"><span data-stu-id="3a18e-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="3a18e-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a18e-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="3a18e-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="3a18e-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="3a18e-114">At the end of this tutorial, you run two Python console apps:</span><span class="sxs-lookup"><span data-stu-id="3a18e-114">At the end of this tutorial, you run two Python console apps:</span></span>

* <span data-ttu-id="3a18e-115">**SimulatedDevice.py**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="3a18e-115">**SimulatedDevice.py**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="3a18e-116">**SendCloudToDeviceMessage.py**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="3a18e-116">**SendCloudToDeviceMessage.py**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="3a18e-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="3a18e-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="3a18e-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3a18e-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 

<span data-ttu-id="3a18e-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="3a18e-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="3a18e-120">[Python 2.x or 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="3a18e-120">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="3a18e-121">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span><span class="sxs-lookup"><span data-stu-id="3a18e-121">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="3a18e-122">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span><span class="sxs-lookup"><span data-stu-id="3a18e-122">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="3a18e-123">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="3a18e-123">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="3a18e-124">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span><span class="sxs-lookup"><span data-stu-id="3a18e-124">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="3a18e-125">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="3a18e-125">An active Azure account.</span></span> <span data-ttu-id="3a18e-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="3a18e-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

> [!NOTE]
> <span data-ttu-id="3a18e-127">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span><span class="sxs-lookup"><span data-stu-id="3a18e-127">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="3a18e-128">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="3a18e-128">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 


## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="3a18e-129">Receive messages in the simulated device app</span><span class="sxs-lookup"><span data-stu-id="3a18e-129">Receive messages in the simulated device app</span></span>
<span data-ttu-id="3a18e-130">In this section, you create a Python console app to simulate the device and receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3a18e-130">In this section, you create a Python console app to simulate the device and receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="3a18e-131">Using a text editor, create a **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-131">Using a text editor, create a **SimulatedDevice.py** file.</span></span>

1. <span data-ttu-id="3a18e-132">Add the following `import` statements and variables at the start of the **SimulatedDevice.py** file:</span><span class="sxs-lookup"><span data-stu-id="3a18e-132">Add the following `import` statements and variables at the start of the **SimulatedDevice.py** file:</span></span>
   
    ```python
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError

    RECEIVE_CONTEXT = 0
    WAIT_COUNT = 10
    RECEIVED_COUNT = 0
    RECEIVE_CALLBACKS = 0
    ```

1. <span data-ttu-id="3a18e-133">Add the following code to **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-133">Add the following code to **SimulatedDevice.py** file.</span></span> <span data-ttu-id="3a18e-134">Replace the "{deviceConnectionString}" placeholder value with the device connection string for the device you created in the [Get started with IoT Hub] tutorial:</span><span class="sxs-lookup"><span data-stu-id="3a18e-134">Replace the "{deviceConnectionString}" placeholder value with the device connection string for the device you created in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```python
    # choose AMQP or AMQP_WS as transport protocol
    PROTOCOL = IoTHubTransportProvider.AMQP
    CONNECTION_STRING = "{deviceConnectionString}"
    ```

1. <span data-ttu-id="3a18e-135">Add the following function to print received messages to the console:</span><span class="sxs-lookup"><span data-stu-id="3a18e-135">Add the following function to print received messages to the console:</span></span>
   
    ```python
    def receive_message_callback(message, counter):
        global RECEIVE_CALLBACKS
        message_buffer = message.get_bytearray()
        size = len(message_buffer)
        print ( "Received Message [%d]:" % counter )
        print ( "    Data: <<<%s>>> & Size=%d" % (message_buffer[:size].decode('utf-8'), size) )
        map_properties = message.properties()
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        counter += 1
        RECEIVE_CALLBACKS += 1
        print ( "    Total calls received: %d" % RECEIVE_CALLBACKS )
        return IoTHubMessageDispositionResult.ACCEPTED

    def iothub_client_init():
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)

        client.set_message_callback(receive_message_callback, RECEIVE_CONTEXT)

        return client

    def print_last_message_time(client):
        try:
            last_message = client.get_last_message_receive_time()
            print ( "Last Message: %s" % time.asctime(time.localtime(last_message)) )
            print ( "Actual time : %s" % time.asctime() )
        except IoTHubClientError as iothub_client_error:
            if iothub_client_error.args[0].result == IoTHubClientResult.INDEFINITE_TIME:
                print ( "No message received" )
            else:
                print ( iothub_client_error )
    ```

1. <span data-ttu-id="3a18e-136">Add the following code to initialize the client and wait to recieve the cloud-to-device message:</span><span class="sxs-lookup"><span data-stu-id="3a18e-136">Add the following code to initialize the client and wait to recieve the cloud-to-device message:</span></span>
   
    ```python
    def iothub_client_init():
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)

        client.set_message_callback(receive_message_callback, RECEIVE_CONTEXT)

        return client

    def iothub_client_sample_run():
        try:
            client = iothub_client_init()

            while True:
                print ( "IoTHubClient waiting for commands, press Ctrl-C to exit" )

                status_counter = 0
                while status_counter <= WAIT_COUNT:
                    status = client.get_send_status()
                    print ( "Send status: %s" % status )
                    time.sleep(10)
                    status_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )

        print_last_message_time(client)
    ```

1. <span data-ttu-id="3a18e-137">Add the following main function:</span><span class="sxs-lookup"><span data-stu-id="3a18e-137">Add the following main function:</span></span>
   
    ```python
    if __name__ == '__main__':
        print ( "Starting the IoT Hub Python sample..." )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_sample_run()
    ```

1. <span data-ttu-id="3a18e-138">Save and close **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-138">Save and close **SimulatedDevice.py** file.</span></span>


## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="3a18e-139">Send a cloud-to-device message</span><span class="sxs-lookup"><span data-stu-id="3a18e-139">Send a cloud-to-device message</span></span>
<span data-ttu-id="3a18e-140">In this section, you create a Python console app that sends cloud-to-device messages to the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="3a18e-140">In this section, you create a Python console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="3a18e-141">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3a18e-141">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="3a18e-142">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3a18e-142">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="3a18e-143">Using a text editor, create a **SendCloudToDeviceMessage.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-143">Using a text editor, create a **SendCloudToDeviceMessage.py** file.</span></span>

1. <span data-ttu-id="3a18e-144">Add the following `import` statements and variables at the start of the **SendCloudToDeviceMessage.py** file:</span><span class="sxs-lookup"><span data-stu-id="3a18e-144">Add the following `import` statements and variables at the start of the **SendCloudToDeviceMessage.py** file:</span></span>
   
    ```python
    import random
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubMessaging, IoTHubMessage, IoTHubError

    OPEN_CONTEXT = 0
    FEEDBACK_CONTEXT = 1
    MESSAGE_COUNT = 1
    AVG_WIND_SPEED = 10.0
    MSG_TXT = "{\"service client sent a message\": %.2f}"
    ```

1. <span data-ttu-id="3a18e-145">Add the following code to **SendCloudToDeviceMessage.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-145">Add the following code to **SendCloudToDeviceMessage.py** file.</span></span> <span data-ttu-id="3a18e-146">Replace the "{IoTHubConnectionString}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3a18e-146">Replace the "{IoTHubConnectionString}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="3a18e-147">Replace the "{deviceId}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span><span class="sxs-lookup"><span data-stu-id="3a18e-147">Replace the "{deviceId}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```python
    CONNECTION_STRING = "{IoTHubConnectionString}"
    DEVICE_ID = "{deviceId}"
    ```

1. <span data-ttu-id="3a18e-148">Add the following function to print feedback messages to the console:</span><span class="sxs-lookup"><span data-stu-id="3a18e-148">Add the following function to print feedback messages to the console:</span></span>
   
    ```python
    def open_complete_callback(context):
        print ( 'open_complete_callback called with context: {0}'.format(context) )

    def send_complete_callback(context, messaging_result):
        context = 0
        print ( 'send_complete_callback called with context : {0}'.format(context) )
        print ( 'messagingResult : {0}'.format(messaging_result) )
    ```

1. <span data-ttu-id="3a18e-149">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span><span class="sxs-lookup"><span data-stu-id="3a18e-149">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```python
    def iothub_messaging_sample_run():
        try:
            iothub_messaging = IoTHubMessaging(CONNECTION_STRING)

            iothub_messaging.open(open_complete_callback, OPEN_CONTEXT)

            for i in range(0, MESSAGE_COUNT):
                print ( 'Sending message: {0}'.format(i) )
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))

                # optional: assign ids
                message.message_id = "message_%d" % i
                message.correlation_id = "correlation_%d" % i
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % i
                prop_map.add("Property", prop_text)

                iothub_messaging.send_async(DEVICE_ID, message, send_complete_callback, i)

            try:
                # Try Python 2.xx first
                raw_input("Press Enter to continue...\n")
            except:
                pass
                # Use Python 3.xx in the case of exception
                input("Press Enter to continue...\n")

            iothub_messaging.close()

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubMessaging sample stopped" )
    ```

1. <span data-ttu-id="3a18e-150">Add the following main function:</span><span class="sxs-lookup"><span data-stu-id="3a18e-150">Add the following main function:</span></span>
   
    ```python
    if __name__ == '__main__':
        print ( "Starting the IoT Hub Service Client Messaging Python sample..." )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_messaging_sample_run()
    ```

1. <span data-ttu-id="3a18e-151">Save and close **SendCloudToDeviceMessage.py** file.</span><span class="sxs-lookup"><span data-stu-id="3a18e-151">Save and close **SendCloudToDeviceMessage.py** file.</span></span>


## <a name="run-the-applications"></a><span data-ttu-id="3a18e-152">Run the applications</span><span class="sxs-lookup"><span data-stu-id="3a18e-152">Run the applications</span></span>
<span data-ttu-id="3a18e-153">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="3a18e-153">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="3a18e-154">Open a command prompt and install the **Azure IoT Hub Device SDK for Python**.</span><span class="sxs-lookup"><span data-stu-id="3a18e-154">Open a command prompt and install the **Azure IoT Hub Device SDK for Python**.</span></span>

    ```
    pip install azure-iothub-device-client
    ```

1. <span data-ttu-id="3a18e-155">At the command prompt, run the following command to listen for cloud-to-device messages:</span><span class="sxs-lookup"><span data-stu-id="3a18e-155">At the command prompt, run the following command to listen for cloud-to-device messages:</span></span>
   
    ```shell
    python SimulatedDevice.py 
    ```
   
    ![Run the simulated device app][img-simulated-device]

1. <span data-ttu-id="3a18e-157">Open a new command prompt and install the **Azure IoT Hub Service SDK for Python**.</span><span class="sxs-lookup"><span data-stu-id="3a18e-157">Open a new command prompt and install the **Azure IoT Hub Service SDK for Python**.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

1. <span data-ttu-id="3a18e-158">At a command prompt, run the following command to send a cloud-to-device message and wait for the message feedback:</span><span class="sxs-lookup"><span data-stu-id="3a18e-158">At a command prompt, run the following command to send a cloud-to-device message and wait for the message feedback:</span></span>
   
    ```shell
    python SendCloudToDeviceMessage.py 
    ```
   
    ![Run the app to send the cloud-to-device command][img-send-command]
   
1. <span data-ttu-id="3a18e-160">Note the message recieved by the device.</span><span class="sxs-lookup"><span data-stu-id="3a18e-160">Note the message recieved by the device.</span></span>

    ![Message received][img-message-recieved]


## <a name="next-steps"></a><span data-ttu-id="3a18e-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a18e-162">Next steps</span></span>
<span data-ttu-id="3a18e-163">In this tutorial, you learned how to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="3a18e-163">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="3a18e-164">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator].</span><span class="sxs-lookup"><span data-stu-id="3a18e-164">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator].</span></span>

<span data-ttu-id="3a18e-165">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="3a18e-165">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-python-python-c2d/simulated-device.png
[img-send-command]:  media/iot-hub-python-python-c2d/send-command.png
[img-message-recieved]: media/iot-hub-python-python-c2d/message-recieved.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[Get started with IoT Hub]: quickstart-send-telemetry-node.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT Hub developer guide]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Remote Monitoring solution accelerator]: https://azure.microsoft.com/documentation/suites/iot-suite/
