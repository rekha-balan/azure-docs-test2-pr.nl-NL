## <a name="create-a-device-identity"></a><span data-ttu-id="d96bf-101">Create a device identity</span><span class="sxs-lookup"><span data-stu-id="d96bf-101">Create a device identity</span></span>
<span data-ttu-id="d96bf-102">In this section, you use a Node.js tool called [IoT Hub Explorer][iot-hub-explorer] to create a device identity for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d96bf-102">In this section, you use a Node.js tool called [IoT Hub Explorer][iot-hub-explorer] to create a device identity for this tutorial.</span></span>

1. <span data-ttu-id="d96bf-103">Run the following in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="d96bf-103">Run the following in your command-line environment:</span></span>
   
    ```
    npm install -g iothub-explorer@latest
    ```
2. <span data-ttu-id="d96bf-104">Then, run the following command to login to your hub.</span><span class="sxs-lookup"><span data-stu-id="d96bf-104">Then, run the following command to login to your hub.</span></span> <span data-ttu-id="d96bf-105">Substitute `{iot hub connection string}` with the IoT Hub connection string you previously copied:</span><span class="sxs-lookup"><span data-stu-id="d96bf-105">Substitute `{iot hub connection string}` with the IoT Hub connection string you previously copied:</span></span>

    ```
    iothub-explorer login "{iot hub connection string}"
    ```
3. <span data-ttu-id="d96bf-106">Finally, create a new device identity called `myDeviceId` with the command:</span><span class="sxs-lookup"><span data-stu-id="d96bf-106">Finally, create a new device identity called `myDeviceId` with the command:</span></span>
   
    ```
    iothub-explorer create myDeviceId --connection-string
    ```

<span data-ttu-id="d96bf-107">Make a note of the device connection string from the result.</span><span class="sxs-lookup"><span data-stu-id="d96bf-107">Make a note of the device connection string from the result.</span></span> <span data-ttu-id="d96bf-108">This device connection string is used by the device app to connect to your IoT Hub as a device.</span><span class="sxs-lookup"><span data-stu-id="d96bf-108">This device connection string is used by the device app to connect to your IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="d96bf-109">Refer to [Getting started with IoT Hub][lnk-getstarted] to programmatically create device identities.</span><span class="sxs-lookup"><span data-stu-id="d96bf-109">Refer to [Getting started with IoT Hub][lnk-getstarted] to programmatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md

