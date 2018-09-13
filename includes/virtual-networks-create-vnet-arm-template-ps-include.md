## <a name="deploy-the-arm-template-by-using-powershell"></a><span data-ttu-id="fcdb4-101">Deploy the ARM template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcdb4-101">Deploy the ARM template by using PowerShell</span></span>
<span data-ttu-id="fcdb4-102">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-102">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="fcdb4-103">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-103">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="fcdb4-104">If necessary, run the **`New-AzureRmResourceGroup`** cmdlet to create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-104">If necessary, run the **`New-AzureRmResourceGroup`** cmdlet to create a new resource group.</span></span> <span data-ttu-id="fcdb4-105">The command below creates a resource group named *TestRG* in the *Central US* azure region.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-105">The command below creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="fcdb4-106">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fcdb4-106">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>
   
        New-AzureRmResourceGroup -Name TestRG -Location centralus
   
    <span data-ttu-id="fcdb4-107">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="fcdb4-107">Here is the expected output for the command above:</span></span>
   
        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
3. <span data-ttu-id="fcdb4-108">Run the **`New-AzureRmResourceGroupDeployment`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-108">Run the **`New-AzureRmResourceGroupDeployment`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span>
   
        New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
            -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
   
    <span data-ttu-id="fcdb4-109">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="fcdb4-109">Here is the expected output for the command above:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : 8/14/2015 9:40:00 PM
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="fcdb4-110">Run the **`Get-AzureRmVirtualNetwork`** cmdlet to view the properties of the new VNet, as shown below.</span><span class="sxs-lookup"><span data-stu-id="fcdb4-110">Run the **`Get-AzureRmVirtualNetwork`** cmdlet to view the properties of the new VNet, as shown below.</span></span>

        Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet

    <span data-ttu-id="fcdb4-111">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="fcdb4-111">Here is the expected output for the command above:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]