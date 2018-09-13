> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="16f52-103">Introduction</span><span class="sxs-lookup"><span data-stu-id="16f52-103">Introduction</span></span>
<span data-ttu-id="16f52-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="16f52-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="16f52-105">Previous tutorials ([Get started with IoT Hub] and [Send Cloud-to-Device messages with IoT Hub]) illustrate the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="16f52-105">Previous tutorials ([Get started with IoT Hub] and [Send Cloud-to-Device messages with IoT Hub]) illustrate the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="16f52-106">IoT Hub also gives you the ability to invoke non-durable methods on devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="16f52-106">IoT Hub also gives you the ability to invoke non-durable methods on devices from the cloud.</span></span> <span data-ttu-id="16f52-107">Methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout) to let the user know the status of the call.</span><span class="sxs-lookup"><span data-stu-id="16f52-107">Methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout) to let the user know the status of the call.</span></span> <span data-ttu-id="16f52-108">[Invoke a direct method on a device][lnk-devguide-methods] describes methods in more detail and offers guidance about when to use methods versus cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="16f52-108">[Invoke a direct method on a device][lnk-devguide-methods] describes methods in more detail and offers guidance about when to use methods versus cloud-to-device messages.</span></span>

<span data-ttu-id="16f52-109">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="16f52-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="16f52-110">Use the Azure portal to create an IoT hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="16f52-110">Use the Azure portal to create an IoT hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="16f52-111">Create a simulated device app that has a direct method which can be called by the cloud.</span><span class="sxs-lookup"><span data-stu-id="16f52-111">Create a simulated device app that has a direct method which can be called by the cloud.</span></span>
* <span data-ttu-id="16f52-112">Create a console app that calls a direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="16f52-112">Create a console app that calls a direct method in the simulated device app through your IoT hub.</span></span>

> [!NOTE]
> At this time, direct methods are accessible only from devices that connect to IoT Hub using the MQTT protocol. Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.
> 
> 




[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[Get started with IoT Hub]: ../articles/iot-hub/iot-hub-node-node-getstarted.md