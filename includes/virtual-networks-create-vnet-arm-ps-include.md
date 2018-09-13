## <a name="how-to-create-a-vnet-using-powershell"></a><span data-ttu-id="feadb-101">How to create a VNet using PowerShell</span><span class="sxs-lookup"><span data-stu-id="feadb-101">How to create a VNet using PowerShell</span></span>
<span data-ttu-id="feadb-102">To create a VNet by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="feadb-102">To create a VNet by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="feadb-103">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="feadb-103">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="feadb-104">If necessary, create a new resource group, as shown below.</span><span class="sxs-lookup"><span data-stu-id="feadb-104">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="feadb-105">For our scenario, create a resource group named *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="feadb-105">For our scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="feadb-106">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="feadb-106">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>
   
        New-AzureRmResourceGroup -Name TestRG -Location centralus
   
    <span data-ttu-id="feadb-107">Expected output:</span><span class="sxs-lookup"><span data-stu-id="feadb-107">Expected output:</span></span>
   
        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG    
3. <span data-ttu-id="feadb-108">Create a new VNet named *TestVNet*, as shown below.</span><span class="sxs-lookup"><span data-stu-id="feadb-108">Create a new VNet named *TestVNet*, as shown below.</span></span>
   
        New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
            -AddressPrefix 192.168.0.0/16 -Location centralus    
   
    <span data-ttu-id="feadb-109">Expected output:</span><span class="sxs-lookup"><span data-stu-id="feadb-109">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="feadb-110">Store the virtual network object in a variable, as shown below.</span><span class="sxs-lookup"><span data-stu-id="feadb-110">Store the virtual network object in a variable, as shown below.</span></span>
   
        $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
   
   > [!TIP]
   > <span data-ttu-id="feadb-111">You can combine steps 3 and 4 by running **$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus**.</span><span class="sxs-lookup"><span data-stu-id="feadb-111">You can combine steps 3 and 4 by running **$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus**.</span></span>
   > 
   > 
5. <span data-ttu-id="feadb-112">Add a subnet to the new VNet variable, as shown below.</span><span class="sxs-lookup"><span data-stu-id="feadb-112">Add a subnet to the new VNet variable, as shown below.</span></span>
   
        Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
            -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
   
    <span data-ttu-id="feadb-113">Expected output:</span><span class="sxs-lookup"><span data-stu-id="feadb-113">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []
6. <span data-ttu-id="feadb-114">Repeat step 5 above for each subnet you want to create.</span><span class="sxs-lookup"><span data-stu-id="feadb-114">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="feadb-115">The command below creates the *BackEnd* subnet for our scenario.</span><span class="sxs-lookup"><span data-stu-id="feadb-115">The command below creates the *BackEnd* subnet for our scenario.</span></span>
   
        Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
            -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
7. <span data-ttu-id="feadb-116">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span><span class="sxs-lookup"><span data-stu-id="feadb-116">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="feadb-117">To save the changes to Azure, run the **Set-AzureRmVirtualNetwork** cmdlet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="feadb-117">To save the changes to Azure, run the **Set-AzureRmVirtualNetwork** cmdlet, as shown below.</span></span>
   
        Set-AzureRmVirtualNetwork -VirtualNetwork $vnet    
   
    <span data-ttu-id="feadb-118">Expected output:</span><span class="sxs-lookup"><span data-stu-id="feadb-118">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                    "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                    "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

