## <a name="create-a-service-namespace"></a><span data-ttu-id="d6378-101">Create a service namespace</span><span class="sxs-lookup"><span data-stu-id="d6378-101">Create a service namespace</span></span>

<span data-ttu-id="d6378-102">To begin using Service Bus queues in Azure, you must first create a namespace.</span><span class="sxs-lookup"><span data-stu-id="d6378-102">To begin using Service Bus queues in Azure, you must first create a namespace.</span></span> <span data-ttu-id="d6378-103">A namespace provides a scoping container for addressing Service Bus resources within your application.</span><span class="sxs-lookup"><span data-stu-id="d6378-103">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span> 

<span data-ttu-id="d6378-104">To create a namespace:</span><span class="sxs-lookup"><span data-stu-id="d6378-104">To create a namespace:</span></span>

1. <span data-ttu-id="d6378-105">Log on to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d6378-105">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d6378-106">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="d6378-106">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="d6378-107">In the **Create namespace** dialog, enter a namespace name.</span><span class="sxs-lookup"><span data-stu-id="d6378-107">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="d6378-108">The system immediately checks to see if the name is available.</span><span class="sxs-lookup"><span data-stu-id="d6378-108">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="d6378-109">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span><span class="sxs-lookup"><span data-stu-id="d6378-109">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="d6378-110">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="d6378-110">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
6. <span data-ttu-id="d6378-111">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="d6378-111">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="d6378-112">In **Location**, choose the country or region in which your namespace should be hosted.</span><span class="sxs-lookup"><span data-stu-id="d6378-112">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
8. <span data-ttu-id="d6378-114">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6378-114">Click **Create**.</span></span> <span data-ttu-id="d6378-115">The system now creates your namespace and enables it.</span><span class="sxs-lookup"><span data-stu-id="d6378-115">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="d6378-116">You might have to wait several minutes as the system provisions resources for your account.</span><span class="sxs-lookup"><span data-stu-id="d6378-116">You might have to wait several minutes as the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="d6378-117">Obtain the management credentials</span><span class="sxs-lookup"><span data-stu-id="d6378-117">Obtain the management credentials</span></span>
1. <span data-ttu-id="d6378-118">In the list of namespaces, click the newly created namespace name.</span><span class="sxs-lookup"><span data-stu-id="d6378-118">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="d6378-119">In the namespace blade, click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="d6378-119">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="d6378-120">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="d6378-120">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="d6378-122">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span><span class="sxs-lookup"><span data-stu-id="d6378-122">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="d6378-123">Paste this value into Notepad or some other temporary location.</span><span class="sxs-lookup"><span data-stu-id="d6378-123">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="d6378-125">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span><span class="sxs-lookup"><span data-stu-id="d6378-125">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com


