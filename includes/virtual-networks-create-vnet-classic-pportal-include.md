## <a name="how-to-create-a-classic-vnet-in-the-azure-portal"></a><span data-ttu-id="e7a02-101">How to create a classic VNet in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e7a02-101">How to create a classic VNet in the Azure portal</span></span>
<span data-ttu-id="e7a02-102">To create a classic VNet based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="e7a02-102">To create a classic VNet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e7a02-103">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="e7a02-103">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="e7a02-104">Click **NEW** > **Networking** > **Virtual network**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**, as seen in the figure below.</span><span class="sxs-lookup"><span data-stu-id="e7a02-104">Click **NEW** > **Networking** > **Virtual network**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Create VNet in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. <span data-ttu-id="e7a02-106">On the **Virtual network** blade, type the **Name** of the VNet, and then click **Address space**.</span><span class="sxs-lookup"><span data-stu-id="e7a02-106">On the **Virtual network** blade, type the **Name** of the VNet, and then click **Address space**.</span></span> <span data-ttu-id="e7a02-107">Configure your address space settings for the VNet and its first subnet, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e7a02-107">Configure your address space settings for the VNet and its first subnet, then click **OK**.</span></span> <span data-ttu-id="e7a02-108">The figure below shows the CIDR block settings for our scenario.</span><span class="sxs-lookup"><span data-stu-id="e7a02-108">The figure below shows the CIDR block settings for our scenario.</span></span>
   
    ![Address space blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. <span data-ttu-id="e7a02-110">Click **Resource Group** and select a resource group to add the VNet to, or click **Create new resource group** to add the VNet to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="e7a02-110">Click **Resource Group** and select a resource group to add the VNet to, or click **Create new resource group** to add the VNet to a new resource group.</span></span> <span data-ttu-id="e7a02-111">The figure below shows the resource group settings for a new resource group called **TestRG**.</span><span class="sxs-lookup"><span data-stu-id="e7a02-111">The figure below shows the resource group settings for a new resource group called **TestRG**.</span></span> <span data-ttu-id="e7a02-112">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e7a02-112">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   
    ![Create resource group blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. <span data-ttu-id="e7a02-114">If necessary, change the **Subscription** and **Location** settings for your VNet.</span><span class="sxs-lookup"><span data-stu-id="e7a02-114">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span> 
6. <span data-ttu-id="e7a02-115">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span><span class="sxs-lookup"><span data-stu-id="e7a02-115">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span> 
7. <span data-ttu-id="e7a02-116">Click **Create** and notice the tile named **Creating Virtual network** as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="e7a02-116">Click **Create** and notice the tile named **Creating Virtual network** as shown in the figure below.</span></span>
   
    ![Create VNet in portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. <span data-ttu-id="e7a02-118">Wait for the VNet to be created, and when you see the tile below, click it to add more subnets.</span><span class="sxs-lookup"><span data-stu-id="e7a02-118">Wait for the VNet to be created, and when you see the tile below, click it to add more subnets.</span></span>
   
    ![Create VNet in portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. <span data-ttu-id="e7a02-120">You should see the **Configuration** for your VNet as shown below.</span><span class="sxs-lookup"><span data-stu-id="e7a02-120">You should see the **Configuration** for your VNet as shown below.</span></span> 
   
    ![Create VNet in portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. <span data-ttu-id="e7a02-122">Click **Subnets** > **Add**, then type a **Name** and specify an **Address range (CIDR block)** for your subnet, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e7a02-122">Click **Subnets** > **Add**, then type a **Name** and specify an **Address range (CIDR block)** for your subnet, and then click **OK**.</span></span> <span data-ttu-id="e7a02-123">The figure below shows the settings for our current scenario.</span><span class="sxs-lookup"><span data-stu-id="e7a02-123">The figure below shows the settings for our current scenario.</span></span>
    
    ![Create VNet in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)








