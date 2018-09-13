## <a name="create-an-iot-hub"></a><span data-ttu-id="f0c06-101">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="f0c06-101">Create an IoT hub</span></span>

1. <span data-ttu-id="f0c06-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Create an iot hub in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
1. <span data-ttu-id="f0c06-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="f0c06-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

   <span data-ttu-id="f0c06-105">**Name**: It is the name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0c06-105">**Name**: It is the name for your IoT hub.</span></span> <span data-ttu-id="f0c06-106">If the name you enter is valid, a green check mark appears.</span><span class="sxs-lookup"><span data-stu-id="f0c06-106">If the name you enter is valid, a green check mark appears.</span></span>

   <span data-ttu-id="f0c06-107">**Pricing and scale tier**: Select the free F1 tier.</span><span class="sxs-lookup"><span data-stu-id="f0c06-107">**Pricing and scale tier**: Select the free F1 tier.</span></span> <span data-ttu-id="f0c06-108">This option is sufficient for this demo.</span><span class="sxs-lookup"><span data-stu-id="f0c06-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="f0c06-109">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="f0c06-109">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

   <span data-ttu-id="f0c06-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="f0c06-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="f0c06-111">See [Using resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f0c06-111">See [Using resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

   <span data-ttu-id="f0c06-112">**Location**: Select the closest location to you where the IoT hub is created.</span><span class="sxs-lookup"><span data-stu-id="f0c06-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

   <span data-ttu-id="f0c06-113">**Pin the dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f0c06-113">**Pin the dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Fill in the fields for creating your Azure IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

1. <span data-ttu-id="f0c06-115">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-115">Click **Create**.</span></span> <span data-ttu-id="f0c06-116">It could take a few minutes for your IoT hub to be created.</span><span class="sxs-lookup"><span data-stu-id="f0c06-116">It could take a few minutes for your IoT hub to be created.</span></span> <span data-ttu-id="f0c06-117">You can see progress in the **Notifications** pane.</span><span class="sxs-lookup"><span data-stu-id="f0c06-117">You can see progress in the **Notifications** pane.</span></span>

   ![See notifications of your IoT hub creation progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

1. <span data-ttu-id="f0c06-119">Once your IoT hub is created, click it from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f0c06-119">Once your IoT hub is created, click it from the dashboard.</span></span> <span data-ttu-id="f0c06-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![Get the hostname of your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

1. <span data-ttu-id="f0c06-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0c06-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="f0c06-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="f0c06-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

   ![Get your IoT hub connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-the-your-device"></a><span data-ttu-id="f0c06-125">Register a device in the IoT hub for the your device</span><span class="sxs-lookup"><span data-stu-id="f0c06-125">Register a device in the IoT hub for the your device</span></span>

1. <span data-ttu-id="f0c06-126">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0c06-126">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>
1. <span data-ttu-id="f0c06-127">Click **Device Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-127">Click **Device Explorer**.</span></span>
1. <span data-ttu-id="f0c06-128">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0c06-128">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span>

   <span data-ttu-id="f0c06-129">**Device ID**: The ID of the new device.</span><span class="sxs-lookup"><span data-stu-id="f0c06-129">**Device ID**: The ID of the new device.</span></span>

   <span data-ttu-id="f0c06-130">**Authentication Type**: Select **Symmetric Key**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-130">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="f0c06-131">**Auto Generate Keys**: Check this field.</span><span class="sxs-lookup"><span data-stu-id="f0c06-131">**Auto Generate Keys**: Check this field.</span></span>

   <span data-ttu-id="f0c06-132">**Connect device to IoT Hub**: Click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-132">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![Add a device in the device explorer of your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

1. <span data-ttu-id="f0c06-134">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f0c06-134">Click **Save**.</span></span>
1. <span data-ttu-id="f0c06-135">After the device is created, open the device in the **Device Explorer** pane.</span><span class="sxs-lookup"><span data-stu-id="f0c06-135">After the device is created, open the device in the **Device Explorer** pane.</span></span>
1. <span data-ttu-id="f0c06-136">Make a note of the primary key of the connection string.</span><span class="sxs-lookup"><span data-stu-id="f0c06-136">Make a note of the primary key of the connection string.</span></span>

   ![Get the device connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)






