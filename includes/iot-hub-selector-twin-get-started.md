> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="eb31d-103">Introduction</span><span class="sxs-lookup"><span data-stu-id="eb31d-103">Introduction</span></span>
<span data-ttu-id="eb31d-104">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span><span class="sxs-lookup"><span data-stu-id="eb31d-104">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="eb31d-105">IoT Hub persists a device twin for each device that connects to it.</span><span class="sxs-lookup"><span data-stu-id="eb31d-105">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="eb31d-106">Use device twins to:</span><span class="sxs-lookup"><span data-stu-id="eb31d-106">Use device twins to:</span></span>

* <span data-ttu-id="eb31d-107">Store device metadata from your solution back end.</span><span class="sxs-lookup"><span data-stu-id="eb31d-107">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="eb31d-108">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span><span class="sxs-lookup"><span data-stu-id="eb31d-108">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="eb31d-109">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span><span class="sxs-lookup"><span data-stu-id="eb31d-109">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="eb31d-110">Query your device metadata, configuration, or state.</span><span class="sxs-lookup"><span data-stu-id="eb31d-110">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> Device twins are designed for synchronization and for querying device configurations and conditions. More informations on when to use device twins can be found in [Understand device twins][lnk-twins].
> 
> 

<span data-ttu-id="eb31d-113">Device twins are stored in an IoT hub and contain:</span><span class="sxs-lookup"><span data-stu-id="eb31d-113">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="eb31d-114">*tags*, device metadata accessible only by the solution back end;</span><span class="sxs-lookup"><span data-stu-id="eb31d-114">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="eb31d-115">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span><span class="sxs-lookup"><span data-stu-id="eb31d-115">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="eb31d-116">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span><span class="sxs-lookup"><span data-stu-id="eb31d-116">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="eb31d-117">Tags and properties cannot contain arrays, but objects can be nested.</span><span class="sxs-lookup"><span data-stu-id="eb31d-117">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="eb31d-118">Additionally, the solution back end can query device twins based on all the above data.</span><span class="sxs-lookup"><span data-stu-id="eb31d-118">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="eb31d-119">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span><span class="sxs-lookup"><span data-stu-id="eb31d-119">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol. Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.
> 
> 

<span data-ttu-id="eb31d-122">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="eb31d-122">This tutorial shows you how to:</span></span>

* <span data-ttu-id="eb31d-123">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span><span class="sxs-lookup"><span data-stu-id="eb31d-123">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="eb31d-124">Query devices from your back-end app using filters on the tags and properties previously created.</span><span class="sxs-lookup"><span data-stu-id="eb31d-124">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md
