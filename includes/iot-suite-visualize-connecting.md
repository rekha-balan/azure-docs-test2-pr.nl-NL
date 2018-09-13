## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="6d057-101">View device telemetry in the dashboard</span><span class="sxs-lookup"><span data-stu-id="6d057-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="6d057-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6d057-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="6d057-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span><span class="sxs-lookup"><span data-stu-id="6d057-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="6d057-104">In the **Devices list**, you should see that the status of your device is **Running**.</span><span class="sxs-lookup"><span data-stu-id="6d057-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="6d057-105">If not, click **Enable Device** in the **Device Details** panel.</span><span class="sxs-lookup"><span data-stu-id="6d057-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![View device status][18]
3. <span data-ttu-id="6d057-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span><span class="sxs-lookup"><span data-stu-id="6d057-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="6d057-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span><span class="sxs-lookup"><span data-stu-id="6d057-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![View device telemetry][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="6d057-110">Invoke a method on your device</span><span class="sxs-lookup"><span data-stu-id="6d057-110">Invoke a method on your device</span></span>
<span data-ttu-id="6d057-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6d057-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="6d057-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span><span class="sxs-lookup"><span data-stu-id="6d057-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="6d057-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span><span class="sxs-lookup"><span data-stu-id="6d057-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="6d057-114">Click **Device ID** for your device in the **Devices list**.</span><span class="sxs-lookup"><span data-stu-id="6d057-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="6d057-115">In the **Device details** panel, click **Methods**.</span><span class="sxs-lookup"><span data-stu-id="6d057-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Device methods][13]
4. <span data-ttu-id="6d057-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span><span class="sxs-lookup"><span data-stu-id="6d057-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="6d057-118">Click **Invoke Method** to call the method on the device.</span><span class="sxs-lookup"><span data-stu-id="6d057-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Invoke a device method][14]
   

5. <span data-ttu-id="6d057-120">You see a message in the console running your device code when the device handles the method.</span><span class="sxs-lookup"><span data-stu-id="6d057-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="6d057-121">The results of the method are added to the history in the solution portal:</span><span class="sxs-lookup"><span data-stu-id="6d057-121">The results of the method are added to the history in the solution portal:</span></span>

    ![View method history][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="6d057-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d057-123">Next steps</span></span>
<span data-ttu-id="6d057-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span><span class="sxs-lookup"><span data-stu-id="6d057-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="6d057-125">Possible extensions include using real sensors and implementing additional commands.</span><span class="sxs-lookup"><span data-stu-id="6d057-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="6d057-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="6d057-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-visualize-connecting/suite4.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-visualize-connecting/suite7-1.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md





