## <a name="how-to-create-a-vnet-in-the-azure-portal"></a><span data-ttu-id="3eee8-101">How to create a VNet in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3eee8-101">How to create a VNet in the Azure portal</span></span>
<span data-ttu-id="3eee8-102">To create a VNet based on the scenario above by using the Azure preview portal, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-102">To create a VNet based on the scenario above by using the Azure preview portal, follow the steps below.</span></span>

1. <span data-ttu-id="3eee8-103">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="3eee8-103">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3eee8-104">Click **NEW** > **Networking** > **Virtual network**, then click **Resource Manager** from the **Select a deployment model** list, and then click **Create**, as seen in the figure below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-104">Click **NEW** > **Networking** > **Virtual network**, then click **Resource Manager** from the **Select a deployment model** list, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Create VNet in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure1.gif)
3. <span data-ttu-id="3eee8-106">On the **Create virtual network** blade, configure the VNet settings as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-106">On the **Create virtual network** blade, configure the VNet settings as shown in the figure below.</span></span>
   
    ![Create virtual network blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure2.png)
4. <span data-ttu-id="3eee8-108">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="3eee8-108">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="3eee8-109">The figure below shows the resource group settings for a new resource group called **TestRG**.</span><span class="sxs-lookup"><span data-stu-id="3eee8-109">The figure below shows the resource group settings for a new resource group called **TestRG**.</span></span> <span data-ttu-id="3eee8-110">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="3eee8-110">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   
    ![Resource group](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure3.png)
5. <span data-ttu-id="3eee8-112">If necessary, change the **Subscription** and **Location** settings for your VNet.</span><span class="sxs-lookup"><span data-stu-id="3eee8-112">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span> 
6. <span data-ttu-id="3eee8-113">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span><span class="sxs-lookup"><span data-stu-id="3eee8-113">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span> 
7. <span data-ttu-id="3eee8-114">Click **Create** and notice the tile named **Creating Virtual network** as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-114">Click **Create** and notice the tile named **Creating Virtual network** as shown in the figure below.</span></span>
   
    ![Creating virtual network tile](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure4.png)
8. <span data-ttu-id="3eee8-116">Wait for the VNet to be created, then in the **Virtual network** blade, click **All settings** > **Subnets** > **Add** as seen below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-116">Wait for the VNet to be created, then in the **Virtual network** blade, click **All settings** > **Subnets** > **Add** as seen below.</span></span>
   
    ![Adding subnet in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure5.gif)
9. <span data-ttu-id="3eee8-118">Specify the subnet settings for the *BackEnd* subnet, as shown below, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eee8-118">Specify the subnet settings for the *BackEnd* subnet, as shown below, and then click **OK**.</span></span> 
   
    ![Subnet settings](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure6.png)
10. <span data-ttu-id="3eee8-120">Notice the list of subnets, as shown in the figure below.</span><span class="sxs-lookup"><span data-stu-id="3eee8-120">Notice the list of subnets, as shown in the figure below.</span></span>
    
    ![List of subnets in VNet](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-networks-create-vnet-arm-pportal-include/vnet-create-arm-pportal-figure7.png)








