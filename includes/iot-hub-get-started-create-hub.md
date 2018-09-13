## <a name="create-an-iot-hub"></a><span data-ttu-id="bc4aa-101">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="bc4aa-101">Create an IoT hub</span></span>
<span data-ttu-id="bc4aa-102">Create an IoT hub for your simulated device app to connect to.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-102">Create an IoT hub for your simulated device app to connect to.</span></span> <span data-ttu-id="bc4aa-103">The following steps show you how to complete this task by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-103">The following steps show you how to complete this task by using the Azure portal.</span></span>

1. <span data-ttu-id="bc4aa-104">Sign in to the [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="bc4aa-104">Sign in to the [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="bc4aa-105">In the Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-105">In the Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Azure portal Jumpbar][1]
1. <span data-ttu-id="bc4aa-107">In the **IoT hub** blade, choose the configuration for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-107">In the **IoT hub** blade, choose the configuration for your IoT hub.</span></span>
   
    ![IoT hub blade][2]
   
   1. <span data-ttu-id="bc4aa-109">In the **Name** box, enter a name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-109">In the **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="bc4aa-110">If the **Name** is valid and available, a green check mark appears in the **Name** box.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-110">If the **Name** is valid and available, a green check mark appears in the **Name** box.</span></span>
   1. <span data-ttu-id="bc4aa-111">Select a [pricing and scale tier][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="bc4aa-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="bc4aa-112">This tutorial does not require a specific tier.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="bc4aa-113">For this tutorial, use the free F1 tier.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-113">For this tutorial, use the free F1 tier.</span></span>
   1. <span data-ttu-id="bc4aa-114">In **Resource group**, either create a resource group, or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="bc4aa-115">For more information, see [Using resource groups to manage your Azure resources][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="bc4aa-115">For more information, see [Using resource groups to manage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="bc4aa-116">In **Location**, select the location to host your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-116">In **Location**, select the location to host your IoT hub.</span></span> <span data-ttu-id="bc4aa-117">For this tutorial, choose your nearest location.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="bc4aa-118">When you have chosen your IoT hub configuration options, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="bc4aa-119">It can take a few minutes for Azure to create your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-119">It can take a few minutes for Azure to create your IoT hub.</span></span> <span data-ttu-id="bc4aa-120">To check the status, you can monitor the progress on the Startboard or in the Notifications panel.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-120">To check the status, you can monitor the progress on the Startboard or in the Notifications panel.</span></span>
   
    ![New IoT hub status][3]
1. <span data-ttu-id="bc4aa-122">When the IoT hub has been created successfully, click the new tile for your IoT hub in the Azure portal to open the blade for the new IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-122">When the IoT hub has been created successfully, click the new tile for your IoT hub in the Azure portal to open the blade for the new IoT hub.</span></span> <span data-ttu-id="bc4aa-123">Make a note of the **Hostname**, and then click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-123">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![New IoT hub blade][4]
1. <span data-ttu-id="bc4aa-125">In the **Shared access policies** blade, click the **iothubowner** policy, and then copy and make note of the IoT Hub connection string in the **iothubowner** blade.</span><span class="sxs-lookup"><span data-stu-id="bc4aa-125">In the **Shared access policies** blade, click the **iothubowner** policy, and then copy and make note of the IoT Hub connection string in the **iothubowner** blade.</span></span> <span data-ttu-id="bc4aa-126">For more information, see [Access control][lnk-access-control] in the "IoT Hub developer guide."</span><span class="sxs-lookup"><span data-stu-id="bc4aa-126">For more information, see [Access control][lnk-access-control] in the "IoT Hub developer guide."</span></span>
   
    ![Shared access policies blade][5]

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md





