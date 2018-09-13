## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="2538c-101">Configure the Node.js simulated device</span><span class="sxs-lookup"><span data-stu-id="2538c-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="2538c-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span><span class="sxs-lookup"><span data-stu-id="2538c-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="2538c-103">Make a note of the IoT Hub hostname, device id, and device key.</span><span class="sxs-lookup"><span data-stu-id="2538c-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="2538c-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span><span class="sxs-lookup"><span data-stu-id="2538c-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="2538c-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span><span class="sxs-lookup"><span data-stu-id="2538c-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="2538c-106">Run `node --version` at a command prompt or in a shell to check the version.</span><span class="sxs-lookup"><span data-stu-id="2538c-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="2538c-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span><span class="sxs-lookup"><span data-stu-id="2538c-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="2538c-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span><span class="sxs-lookup"><span data-stu-id="2538c-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="2538c-109">Always use the **master** branch for the latest version of the libraries and samples.</span><span class="sxs-lookup"><span data-stu-id="2538c-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="2538c-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span><span class="sxs-lookup"><span data-stu-id="2538c-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="2538c-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="2538c-111">packages.json</span></span>
   * <span data-ttu-id="2538c-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="2538c-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="2538c-113">Open the remote_monitoring.js file and look for the following variable definition:</span><span class="sxs-lookup"><span data-stu-id="2538c-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="2538c-114">Replace **[IoT Hub device connection string]** with your device connection string.</span><span class="sxs-lookup"><span data-stu-id="2538c-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="2538c-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span><span class="sxs-lookup"><span data-stu-id="2538c-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="2538c-116">A device connection string has the following format:</span><span class="sxs-lookup"><span data-stu-id="2538c-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="2538c-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="2538c-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Save the file. <span data-ttu-id="2538c-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span><span class="sxs-lookup"><span data-stu-id="2538c-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="2538c-120">Observe dynamic telemetry in action</span><span class="sxs-lookup"><span data-stu-id="2538c-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="2538c-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span><span class="sxs-lookup"><span data-stu-id="2538c-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![The default dashboard][image1]

<span data-ttu-id="2538c-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span><span class="sxs-lookup"><span data-stu-id="2538c-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Add external temperature to the dashboard][image2]

<span data-ttu-id="2538c-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="2538c-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-send-external-temperature/image1.png
[image2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-suite-send-external-temperature/image2.png

