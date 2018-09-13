## <a name="create-a-device-identity"></a><span data-ttu-id="4530c-101">Create a device identity</span><span class="sxs-lookup"><span data-stu-id="4530c-101">Create a device identity</span></span>

<span data-ttu-id="4530c-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4530c-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="4530c-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="4530c-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="4530c-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="4530c-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="4530c-105">When you run this console app, it generates a unique device ID and key.</span><span class="sxs-lookup"><span data-stu-id="4530c-105">When you run this console app, it generates a unique device ID and key.</span></span> <span data-ttu-id="4530c-106">Your device uses these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4530c-106">Your device uses these values to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="4530c-107">Device IDs are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="4530c-107">Device IDs are case-sensitive.</span></span>

1. <span data-ttu-id="4530c-108">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="4530c-108">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="4530c-109">Make sure the .NET Framework version is 4.5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="4530c-109">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="4530c-110">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="4530c-110">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>

    ![New Visual C# Windows Classic Desktop project][10]

1. <span data-ttu-id="4530c-112">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="4530c-112">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="4530c-113">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="4530c-113">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="4530c-114">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="4530c-114">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Package Manager window][11]

1. <span data-ttu-id="4530c-116">Add the following `using` statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="4530c-116">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Common.Exceptions;
    ```

1. <span data-ttu-id="4530c-117">Add the following fields to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="4530c-117">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="4530c-118">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4530c-118">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static RegistryManager registryManager;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="4530c-119">Add the following method to the **Program** class:</span><span class="sxs-lookup"><span data-stu-id="4530c-119">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async Task AddDeviceAsync()
    {
      string deviceId = "myFirstDevice";
      Device device;
      try
      {
          device = await registryManager.AddDeviceAsync(new Device(deviceId));
      }
      catch (DeviceAlreadyExistsException)
      {
          device = await registryManager.GetDeviceAsync(deviceId);
      }
      Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
    }
    ```

    <span data-ttu-id="4530c-120">This method creates a device identity with ID **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="4530c-120">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="4530c-121">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span><span class="sxs-lookup"><span data-stu-id="4530c-121">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="4530c-122">You use this key in the simulated device app to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4530c-122">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="4530c-123">Finally, add the following lines to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="4530c-123">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    registryManager = RegistryManager.CreateFromConnectionString(connectionString);
    AddDeviceAsync().Wait();
    Console.ReadLine();
    ```

1. <span data-ttu-id="4530c-124">Run this application, and make a note of the device key.</span><span class="sxs-lookup"><span data-stu-id="4530c-124">Run this application, and make a note of the device key.</span></span>

    ![Device key generated by the application][12]

> [!NOTE]
> <span data-ttu-id="4530c-126">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4530c-126">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="4530c-127">The identity registry stores device IDs and keys to use as security credentials.</span><span class="sxs-lookup"><span data-stu-id="4530c-127">The identity registry stores device IDs and keys to use as security credentials.</span></span> <span data-ttu-id="4530c-128">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span><span class="sxs-lookup"><span data-stu-id="4530c-128">The identity registry also stores an enabled/disabled flag for each device that you can use to disable access for that device.</span></span> <span data-ttu-id="4530c-129">If your application needs to store other device-specific metadata, it should use an application-specific store.</span><span class="sxs-lookup"><span data-stu-id="4530c-129">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="4530c-130">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="4530c-130">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png

<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
