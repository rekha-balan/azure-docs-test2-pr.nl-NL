1. <span data-ttu-id="fd4ab-101">Log on to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="fd4ab-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="fd4ab-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="fd4ab-103">In the **Create namespace** dialog, enter a namespace name.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="fd4ab-104">The system immediately checks to see if the name is available.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="fd4ab-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="fd4ab-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="fd4ab-107">In **Location**, choose the country or region in which your namespace should be hosted.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
7. <span data-ttu-id="fd4ab-109">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-109">Click **Create**.</span></span> <span data-ttu-id="fd4ab-110">The system now creates your namespace and enables it.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="fd4ab-111">After a few minutes, the system provisions resources for your account.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="fd4ab-112">Obtain the management credentials</span><span class="sxs-lookup"><span data-stu-id="fd4ab-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="fd4ab-113">In the list of namespaces, click the newly created namespace name.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="fd4ab-114">In the namespace blade, click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="fd4ab-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="fd4ab-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="fd4ab-118">Paste this value into Notepad or some other temporary location.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="fd4ab-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span><span class="sxs-lookup"><span data-stu-id="fd4ab-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/relay-create-namespace-portal/create-namespace.png
[connection-info]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/relay-create-namespace-portal/connection-info.png
[connection-string]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com



