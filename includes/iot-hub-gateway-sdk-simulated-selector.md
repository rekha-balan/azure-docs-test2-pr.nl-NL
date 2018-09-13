> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-gateway-sdk-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-gateway-sdk-simulated-device.md)
> 
> 

<span data-ttu-id="ed995-103">This walkthrough of the [Simulated Device Cloud Upload sample] shows how to use the [Azure IoT Gateway SDK][lnk-sdk] to send device-to-cloud telemetry to IoT Hub from simulated devices.</span><span class="sxs-lookup"><span data-stu-id="ed995-103">This walkthrough of the [Simulated Device Cloud Upload sample] shows how to use the [Azure IoT Gateway SDK][lnk-sdk] to send device-to-cloud telemetry to IoT Hub from simulated devices.</span></span>

<span data-ttu-id="ed995-104">This walkthrough covers:</span><span class="sxs-lookup"><span data-stu-id="ed995-104">This walkthrough covers:</span></span>

1. <span data-ttu-id="ed995-105">**Architecture**: important architectural information about the Simulated Device Cloud Upload sample.</span><span class="sxs-lookup"><span data-stu-id="ed995-105">**Architecture**: important architectural information about the Simulated Device Cloud Upload sample.</span></span>
2. <span data-ttu-id="ed995-106">**Build and run**: the steps required to build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="ed995-106">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="ed995-107">Architecture</span><span class="sxs-lookup"><span data-stu-id="ed995-107">Architecture</span></span>
<span data-ttu-id="ed995-108">The Simulated Device Cloud Upload sample shows how to use the SDK to create a gateway which sends telemetry from simulated devices to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-108">The Simulated Device Cloud Upload sample shows how to use the SDK to create a gateway which sends telemetry from simulated devices to an IoT hub.</span></span> <span data-ttu-id="ed995-109">The simulated devices cannot connect directly to IoT Hub because:</span><span class="sxs-lookup"><span data-stu-id="ed995-109">The simulated devices cannot connect directly to IoT Hub because:</span></span>

* <span data-ttu-id="ed995-110">The devices do not use a communications protocol understood by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-110">The devices do not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="ed995-111">The devices are not smart enough to remember the identity assigned to them by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-111">The devices are not smart enough to remember the identity assigned to them by IoT Hub.</span></span>

<span data-ttu-id="ed995-112">The gateway solves these problems for the simulated devices in the following ways:</span><span class="sxs-lookup"><span data-stu-id="ed995-112">The gateway solves these problems for the simulated devices in the following ways:</span></span>

* <span data-ttu-id="ed995-113">The gateway understands the protocol used by the simulated devices, receives device-to-cloud telemetry from the devices, and forwards those messages to IoT Hub using a protocol understood by the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-113">The gateway understands the protocol used by the simulated devices, receives device-to-cloud telemetry from the devices, and forwards those messages to IoT Hub using a protocol understood by the IoT hub.</span></span>
* <span data-ttu-id="ed995-114">The gateway stores IoT Hub identities on behalf of the simulated devices and acts as a proxy when the simulated devices send messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-114">The gateway stores IoT Hub identities on behalf of the simulated devices and acts as a proxy when the simulated devices send messages to IoT Hub.</span></span>

<span data-ttu-id="ed995-115">The following diagram shows the main components of the sample, including the gateway modules:</span><span class="sxs-lookup"><span data-stu-id="ed995-115">The following diagram shows the main components of the sample, including the gateway modules:</span></span>

![][1]

> [!NOTE]
> The modules do not pass messages directly to each other. The modules publish messages to an internal broker that delivers the messages to the other modules using a subscription mechanism as shown in the diagram below. For more information, see [Get started with the IoT Gateway SDK][lnk-gw-getstarted].
> 
> 

### <a name="protocol-ingestion-module"></a><span data-ttu-id="ed995-119">Protocol ingestion module</span><span class="sxs-lookup"><span data-stu-id="ed995-119">Protocol ingestion module</span></span>
<span data-ttu-id="ed995-120">This module is the starting point for getting data from devices, through the gateway, and into the cloud.</span><span class="sxs-lookup"><span data-stu-id="ed995-120">This module is the starting point for getting data from devices, through the gateway, and into the cloud.</span></span> <span data-ttu-id="ed995-121">In the sample, the module performs four tasks:</span><span class="sxs-lookup"><span data-stu-id="ed995-121">In the sample, the module performs four tasks:</span></span>

1. <span data-ttu-id="ed995-122">It creates simulated temperature data.</span><span class="sxs-lookup"><span data-stu-id="ed995-122">It creates simulated temperature data.</span></span> <span data-ttu-id="ed995-123">Note that if you use real devices, the module reads data from those physical devices.</span><span class="sxs-lookup"><span data-stu-id="ed995-123">Note that if you use real devices, the module reads data from those physical devices.</span></span>
2. <span data-ttu-id="ed995-124">It places the simulated temperature data into the contents of a message.</span><span class="sxs-lookup"><span data-stu-id="ed995-124">It places the simulated temperature data into the contents of a message.</span></span>
3. <span data-ttu-id="ed995-125">It adds a property with a fake MAC address to the message that contains the simulated temperature data.</span><span class="sxs-lookup"><span data-stu-id="ed995-125">It adds a property with a fake MAC address to the message that contains the simulated temperature data.</span></span>
4. <span data-ttu-id="ed995-126">It makes the message available to the next module in the chain.</span><span class="sxs-lookup"><span data-stu-id="ed995-126">It makes the message available to the next module in the chain.</span></span>

> [!NOTE]
> The module called **Protocol X ingestion** in the diagram above is called **Simulated device** in the source code.
> 
> 

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="ed995-128">MAC &lt;-&gt; IoT Hub ID module</span><span class="sxs-lookup"><span data-stu-id="ed995-128">MAC &lt;-&gt; IoT Hub ID module</span></span>
<span data-ttu-id="ed995-129">This module scans for messages that include a property that contains the MAC address, added by the protocol ingestion module, of the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="ed995-129">This module scans for messages that include a property that contains the MAC address, added by the protocol ingestion module, of the simulated device app.</span></span> <span data-ttu-id="ed995-130">If the module finds such a property, it adds another property with an IoT Hub device key to the message and then makes the message available to the next module in the chain.</span><span class="sxs-lookup"><span data-stu-id="ed995-130">If the module finds such a property, it adds another property with an IoT Hub device key to the message and then makes the message available to the next module in the chain.</span></span> <span data-ttu-id="ed995-131">This is how the sample associates IoT Hub device identities with simulated devices.</span><span class="sxs-lookup"><span data-stu-id="ed995-131">This is how the sample associates IoT Hub device identities with simulated devices.</span></span> <span data-ttu-id="ed995-132">The developer sets up the mapping between MAC addresses and IoT Hub identities manually as part of the module configuration.</span><span class="sxs-lookup"><span data-stu-id="ed995-132">The developer sets up the mapping between MAC addresses and IoT Hub identities manually as part of the module configuration.</span></span> 

> [!NOTE]
> This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity. However, you can write your own module that uses a different unique identifier. For example, you may have devices with unique serial numbers or telemetry data that has a unique device name embedded in it that you could use to determine the IoT Hub device identity.
> 
> 

### <a name="iot-hub-communication-module"></a><span data-ttu-id="ed995-136">IoT Hub communication module</span><span class="sxs-lookup"><span data-stu-id="ed995-136">IoT Hub communication module</span></span>
<span data-ttu-id="ed995-137">This module takes messages with an IoT Hub device identity assigned by the previous module and sends the message content to IoT Hub using HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed995-137">This module takes messages with an IoT Hub device identity assigned by the previous module and sends the message content to IoT Hub using HTTP.</span></span> <span data-ttu-id="ed995-138">HTTP is one of the three protocols understood by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed995-138">HTTP is one of the three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="ed995-139">Instead of opening a connection to IoT Hub for each simulated device app, this module opens a single HTTP connection from the gateway to the IoT hub and multiplexes connections from all the simulated devices over that connection.</span><span class="sxs-lookup"><span data-stu-id="ed995-139">Instead of opening a connection to IoT Hub for each simulated device app, this module opens a single HTTP connection from the gateway to the IoT hub and multiplexes connections from all the simulated devices over that connection.</span></span> <span data-ttu-id="ed995-140">This enables a single gateway to connect many more devices, simulated or otherwise, than would be possible if it opened a unique connection for every device.</span><span class="sxs-lookup"><span data-stu-id="ed995-140">This enables a single gateway to connect many more devices, simulated or otherwise, than would be possible if it opened a unique connection for every device.</span></span>

![][2]

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-simulated-selector/image1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-simulated-selector/image2.png

<!-- Links -->
[Simulated Device Cloud Upload sample]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/azure-iot-gateway-sdk
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-gateway-sdk-get-started.md

