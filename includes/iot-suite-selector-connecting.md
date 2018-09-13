> [!div class="op_single_selector"]
> * [C on Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C on Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [C on mbed](../articles/iot-suite/iot-suite-connecting-devices-mbed.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="9942b-105">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="9942b-105">Scenario overview</span></span>
<span data-ttu-id="9942b-106">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="9942b-106">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="9942b-107">External temperature</span><span class="sxs-lookup"><span data-stu-id="9942b-107">External temperature</span></span>
* <span data-ttu-id="9942b-108">Internal temperature</span><span class="sxs-lookup"><span data-stu-id="9942b-108">Internal temperature</span></span>
* <span data-ttu-id="9942b-109">Humidity</span><span class="sxs-lookup"><span data-stu-id="9942b-109">Humidity</span></span>

<span data-ttu-id="9942b-110">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span><span class="sxs-lookup"><span data-stu-id="9942b-110">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="9942b-111">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="9942b-111">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="9942b-112">To complete this tutorial, you need an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="9942b-112">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="9942b-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="9942b-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9942b-114">For details, see [Azure Free Trial][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="9942b-114">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9942b-115">Before you start</span><span class="sxs-lookup"><span data-stu-id="9942b-115">Before you start</span></span>
<span data-ttu-id="9942b-116">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span><span class="sxs-lookup"><span data-stu-id="9942b-116">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9942b-117">Provision your remote monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="9942b-117">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="9942b-118">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="9942b-118">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="9942b-119">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="9942b-119">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="9942b-120">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span><span class="sxs-lookup"><span data-stu-id="9942b-120">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="9942b-121">Click **Select** on the **Remote monitoring** panel to create your solution.</span><span class="sxs-lookup"><span data-stu-id="9942b-121">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="9942b-122">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span><span class="sxs-lookup"><span data-stu-id="9942b-122">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="9942b-123">Then click **Create solution**.</span><span class="sxs-lookup"><span data-stu-id="9942b-123">Then click **Create solution**.</span></span>
4. <span data-ttu-id="9942b-124">Wait until the provisioning process completes.</span><span class="sxs-lookup"><span data-stu-id="9942b-124">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> The preconfigured solutions use billable Azure services. Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges. You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.
> 
> 

<span data-ttu-id="9942b-128">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span><span class="sxs-lookup"><span data-stu-id="9942b-128">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Solution dashboard][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="9942b-130">Provision your device in the remote monitoring solution</span><span class="sxs-lookup"><span data-stu-id="9942b-130">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> If you have already provisioned a device in your solution, you can skip this step. You need to know the device credentials when you create the client application.
> 
> 

<span data-ttu-id="9942b-133">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span><span class="sxs-lookup"><span data-stu-id="9942b-133">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="9942b-134">You can retrieve the device credentials from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="9942b-134">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="9942b-135">You include the device credentials in your client application later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9942b-135">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="9942b-136">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span><span class="sxs-lookup"><span data-stu-id="9942b-136">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="9942b-137">In the lower left-hand corner of the dashboard, click **Add a device**.</span><span class="sxs-lookup"><span data-stu-id="9942b-137">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Add a device][1]
2. <span data-ttu-id="9942b-139">In the **Custom Device** panel, click **Add new**.</span><span class="sxs-lookup"><span data-stu-id="9942b-139">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Add a custom device][2]
3. <span data-ttu-id="9942b-141">Choose **Let me define my own Device ID**.</span><span class="sxs-lookup"><span data-stu-id="9942b-141">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="9942b-142">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span><span class="sxs-lookup"><span data-stu-id="9942b-142">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Add device ID][3]
4. <span data-ttu-id="9942b-144">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span><span class="sxs-lookup"><span data-stu-id="9942b-144">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="9942b-145">Your client application needs these values to connect to the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="9942b-145">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="9942b-146">Then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="9942b-146">Then click **Done**.</span></span>
   
    ![View device credentials][4]
5. <span data-ttu-id="9942b-148">Select your device in the device list in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="9942b-148">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="9942b-149">Then, in the **Device Details** panel, click **Enable Device**.</span><span class="sxs-lookup"><span data-stu-id="9942b-149">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="9942b-150">The status of your device is now **Running**.</span><span class="sxs-lookup"><span data-stu-id="9942b-150">The status of your device is now **Running**.</span></span> <span data-ttu-id="9942b-151">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span><span class="sxs-lookup"><span data-stu-id="9942b-151">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-selector-connecting/dashboard.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-selector-connecting/suite0.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-selector-connecting/suite1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-selector-connecting/suite2.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/




