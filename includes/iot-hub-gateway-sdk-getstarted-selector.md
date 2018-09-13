> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-gateway-sdk-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-gateway-sdk-get-started.md)
> 
> 

<span data-ttu-id="b2f93-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Gateway SDK][lnk-gateway-sdk] architecture.</span><span class="sxs-lookup"><span data-stu-id="b2f93-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Gateway SDK][lnk-gateway-sdk] architecture.</span></span> <span data-ttu-id="b2f93-104">The sample uses the Azure IoT Gateway SDK to build a simple gateway that logs a "hello world" message to a file every five seconds.</span><span class="sxs-lookup"><span data-stu-id="b2f93-104">The sample uses the Azure IoT Gateway SDK to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="b2f93-105">This walkthrough covers:</span><span class="sxs-lookup"><span data-stu-id="b2f93-105">This walkthrough covers:</span></span>

* <span data-ttu-id="b2f93-106">**Concepts**: A conceptual overview of the components that compose any gateway you create with the IoT Gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="b2f93-106">**Concepts**: A conceptual overview of the components that compose any gateway you create with the IoT Gateway SDK.</span></span>  
* <span data-ttu-id="b2f93-107">**Hello World sample architecture**: Describes how the concepts apply to the Hello World sample and how the components fit together.</span><span class="sxs-lookup"><span data-stu-id="b2f93-107">**Hello World sample architecture**: Describes how the concepts apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="b2f93-108">**How to build the sample**: The steps required to build the sample.</span><span class="sxs-lookup"><span data-stu-id="b2f93-108">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="b2f93-109">**How to run the sample**: The steps required to run the sample.</span><span class="sxs-lookup"><span data-stu-id="b2f93-109">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="b2f93-110">**Typical output**: An example of the output to expect when you run the sample.</span><span class="sxs-lookup"><span data-stu-id="b2f93-110">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="b2f93-111">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key gateway components.</span><span class="sxs-lookup"><span data-stu-id="b2f93-111">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key gateway components.</span></span>

## <a name="azure-iot-gateway-sdk-concepts"></a><span data-ttu-id="b2f93-112">Azure IoT Gateway SDK concepts</span><span class="sxs-lookup"><span data-stu-id="b2f93-112">Azure IoT Gateway SDK concepts</span></span>
<span data-ttu-id="b2f93-113">Before you examine the sample code or create your own field gateway using the IoT Gateway SDK, you should understand the key concepts that underpin the architecture of the SDK.</span><span class="sxs-lookup"><span data-stu-id="b2f93-113">Before you examine the sample code or create your own field gateway using the IoT Gateway SDK, you should understand the key concepts that underpin the architecture of the SDK.</span></span>

### <a name="modules"></a><span data-ttu-id="b2f93-114">Modules</span><span class="sxs-lookup"><span data-stu-id="b2f93-114">Modules</span></span>
<span data-ttu-id="b2f93-115">You build a gateway with the Azure IoT Gateway SDK by creating and assembling *modules*.</span><span class="sxs-lookup"><span data-stu-id="b2f93-115">You build a gateway with the Azure IoT Gateway SDK by creating and assembling *modules*.</span></span> <span data-ttu-id="b2f93-116">Modules use *messages* to exchange data with each other.</span><span class="sxs-lookup"><span data-stu-id="b2f93-116">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="b2f93-117">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span><span class="sxs-lookup"><span data-stu-id="b2f93-117">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="b2f93-118">Some modules might only produce new messages and never process incoming messages.</span><span class="sxs-lookup"><span data-stu-id="b2f93-118">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="b2f93-119">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2f93-119">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![A chain of modules in gateway built with the Azure IoT Gateway SDK][1]

<span data-ttu-id="b2f93-121">The SDK contains the following:</span><span class="sxs-lookup"><span data-stu-id="b2f93-121">The SDK contains the following:</span></span>

* <span data-ttu-id="b2f93-122">Pre-written modules which perform common gateway functions.</span><span class="sxs-lookup"><span data-stu-id="b2f93-122">Pre-written modules which perform common gateway functions.</span></span>
* <span data-ttu-id="b2f93-123">The interfaces a developer can use to write custom modules.</span><span class="sxs-lookup"><span data-stu-id="b2f93-123">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="b2f93-124">The infrastructure necessary to deploy and run a set of modules.</span><span class="sxs-lookup"><span data-stu-id="b2f93-124">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="b2f93-125">The SDK provides an abstraction layer that enables you to build gateways to run on a variety of operating systems and platforms.</span><span class="sxs-lookup"><span data-stu-id="b2f93-125">The SDK provides an abstraction layer that enables you to build gateways to run on a variety of operating systems and platforms.</span></span>

![Azure IoT Gateway SDK abstraction layer][2]

### <a name="messages"></a><span data-ttu-id="b2f93-127">Messages</span><span class="sxs-lookup"><span data-stu-id="b2f93-127">Messages</span></span>
<span data-ttu-id="b2f93-128">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span><span class="sxs-lookup"><span data-stu-id="b2f93-128">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="b2f93-129">Modules use a broker to communicate with each other, they publish messages to the broker (bus, pubsub, or any other messaging pattern) and then let the broker route the message to the modules connected to it.</span><span class="sxs-lookup"><span data-stu-id="b2f93-129">Modules use a broker to communicate with each other, they publish messages to the broker (bus, pubsub, or any other messaging pattern) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="b2f93-130">A module uses the **Broker_Publish** function to publish a message to the broker.</span><span class="sxs-lookup"><span data-stu-id="b2f93-130">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="b2f93-131">The broker delivers messages to a module by invoking a callback function.</span><span class="sxs-lookup"><span data-stu-id="b2f93-131">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="b2f93-132">A message consists of a set of key/value properties and content passed as a block of memory.</span><span class="sxs-lookup"><span data-stu-id="b2f93-132">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![The role of the Broker in the Azure IoT Gateway SDK][3]

### <a name="message-routing-and-filtering"></a><span data-ttu-id="b2f93-134">Message routing and filtering</span><span class="sxs-lookup"><span data-stu-id="b2f93-134">Message routing and filtering</span></span>
<span data-ttu-id="b2f93-135">There are two ways of directing messages to the correct modules.</span><span class="sxs-lookup"><span data-stu-id="b2f93-135">There are two ways of directing messages to the correct modules.</span></span> <span data-ttu-id="b2f93-136">A set of links can be passed to the broker so the broker knows the source and sink for each module, or the module can filter on the properties of the message.</span><span class="sxs-lookup"><span data-stu-id="b2f93-136">A set of links can be passed to the broker so the broker knows the source and sink for each module, or the module can filter on the properties of the message.</span></span> <span data-ttu-id="b2f93-137">A module should only act upon a message if the message is intended for it.</span><span class="sxs-lookup"><span data-stu-id="b2f93-137">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="b2f93-138">The links and message filtering is what effectively creates a message pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2f93-138">The links and message filtering is what effectively creates a message pipeline.</span></span>

## <a name="hello-world-sample-architecture"></a><span data-ttu-id="b2f93-139">Hello World sample architecture</span><span class="sxs-lookup"><span data-stu-id="b2f93-139">Hello World sample architecture</span></span>
<span data-ttu-id="b2f93-140">The Hello World sample illustrates the concepts described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="b2f93-140">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="b2f93-141">The Hello World sample implements a gateway that has a pipeline made up of two modules:</span><span class="sxs-lookup"><span data-stu-id="b2f93-141">The Hello World sample implements a gateway that has a pipeline made up of two modules:</span></span>

* <span data-ttu-id="b2f93-142">The *hello world* module creates a message every five seconds and passes it to the logger module.</span><span class="sxs-lookup"><span data-stu-id="b2f93-142">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="b2f93-143">The *logger* module writes the messages it receives to a file.</span><span class="sxs-lookup"><span data-stu-id="b2f93-143">The *logger* module writes the messages it receives to a file.</span></span>

![Architecture of Hello World sample built with the Azure IoT Gateway SDK][4]

<span data-ttu-id="b2f93-145">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span><span class="sxs-lookup"><span data-stu-id="b2f93-145">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="b2f93-146">Instead, it publishes a message to the broker every five seconds.</span><span class="sxs-lookup"><span data-stu-id="b2f93-146">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="b2f93-147">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span><span class="sxs-lookup"><span data-stu-id="b2f93-147">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="b2f93-148">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span><span class="sxs-lookup"><span data-stu-id="b2f93-148">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![How the broker routes messages between modules in the Azure IoT Gateway SDK][5]

<span data-ttu-id="b2f93-150">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-gateway-sdk].</span><span class="sxs-lookup"><span data-stu-id="b2f93-150">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-gateway-sdk].</span></span> <span data-ttu-id="b2f93-151">Explore the code on your own, or use the code snippets below as a guide.</span><span class="sxs-lookup"><span data-stu-id="b2f93-151">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-getstarted-selector/modules.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-getstarted-selector/modules_2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-getstarted-selector/messages_1.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-getstarted-selector/high_level_architecture.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-gateway-sdk-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/hello_world
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk




