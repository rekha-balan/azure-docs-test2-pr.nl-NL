## <a name="how-to-create-a-vnet-using-a-network-config-file-from-powershell"></a><span data-ttu-id="bc57d-101">How to create a VNet using a network config file from PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc57d-101">How to create a VNet using a network config file from PowerShell</span></span>
<span data-ttu-id="bc57d-102">Azure uses an xml file to define all VNets available to a subscription.</span><span class="sxs-lookup"><span data-stu-id="bc57d-102">Azure uses an xml file to define all VNets available to a subscription.</span></span> <span data-ttu-id="bc57d-103">You can download this file, and edit it to modify or delete existing VNets, and create new ones.</span><span class="sxs-lookup"><span data-stu-id="bc57d-103">You can download this file, and edit it to modify or delete existing VNets, and create new ones.</span></span> <span data-ttu-id="bc57d-104">In this document, you will learn how to download this file, referred to as network configuration (or netcgf) file, and edit it to create a new VNet.</span><span class="sxs-lookup"><span data-stu-id="bc57d-104">In this document, you will learn how to download this file, referred to as network configuration (or netcgf) file, and edit it to create a new VNet.</span></span> <span data-ttu-id="bc57d-105">Check the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) to learn more about the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="bc57d-105">Check the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) to learn more about the network configuration file.</span></span>

<span data-ttu-id="bc57d-106">To create a VNet using a netcfg file using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="bc57d-106">To create a VNet using a netcfg file using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="bc57d-107">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="bc57d-107">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="bc57d-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file by running the command below.</span><span class="sxs-lookup"><span data-stu-id="bc57d-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file by running the command below.</span></span> 
   
        Get-AzureVNetConfig -ExportToFile c:\NetworkConfig.xml
   
    <span data-ttu-id="bc57d-109">Expected output:</span><span class="sxs-lookup"><span data-stu-id="bc57d-109">Expected output:</span></span>
   
        XMLConfiguration                                                                                                     
        ----------------                                                                                                     
        <?xml version="1.0" encoding="utf-8"?>...  
3. <span data-ttu-id="bc57d-110">Open the file you saved in step 2 above using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span><span class="sxs-lookup"><span data-stu-id="bc57d-110">Open the file you saved in step 2 above using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="bc57d-111">If you have any networks already created, each network will be displayed as its own **<VirtualNetworkSite>** element.</span><span class="sxs-lookup"><span data-stu-id="bc57d-111">If you have any networks already created, each network will be displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="bc57d-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span><span class="sxs-lookup"><span data-stu-id="bc57d-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>
   
        <VirtualNetworkSite name="TestVNet" Location="Central US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
5. <span data-ttu-id="bc57d-113">Save the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="bc57d-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="bc57d-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the command below.</span><span class="sxs-lookup"><span data-stu-id="bc57d-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the command below.</span></span> <span data-ttu-id="bc57d-115">Notice the output under the command, you should see **Succeeded** under **OperationStatus**.</span><span class="sxs-lookup"><span data-stu-id="bc57d-115">Notice the output under the command, you should see **Succeeded** under **OperationStatus**.</span></span> <span data-ttu-id="bc57d-116">If that is not the case, check the xml file for errors.</span><span class="sxs-lookup"><span data-stu-id="bc57d-116">If that is not the case, check the xml file for errors.</span></span>
   
       Set-AzureVNetConfig -ConfigurationPath c:\NetworkConfig.xml
   
   <span data-ttu-id="bc57d-117">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="bc57d-117">Here is the expected output for the command above:</span></span>
   
       OperationDescription OperationId                          OperationStatus
       -------------------- -----------                          ---------------
       Set-AzureVNetConfig  49579cb9-3f49-07c3-ada2-7abd0e28c4e4 Succeeded 
7. <span data-ttu-id="bc57d-118">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the command below.</span><span class="sxs-lookup"><span data-stu-id="bc57d-118">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the command below.</span></span> 
   
       Get-AzureVNetSite -VNetName TestVNet
   
   <span data-ttu-id="bc57d-119">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="bc57d-119">Here is the expected output for the command above:</span></span>
   
       AddressSpacePrefixes : {192.168.0.0/16}
       Location             : Central US
       AffinityGroup        : 
       DnsServers           : {}
       GatewayProfile       : 
       GatewaySites         : 
       Id                   : b953f47b-fad9-4075-8cfe-73ff9c98278f
       InUse                : False
       Label                : 
       Name                 : TestVNet
       State                : Created
       Subnets              : {FrontEnd, BackEnd}
       OperationDescription : Get-AzureVNetSite
       OperationId          : 3f35d533-1f38-09c0-b286-3d07cd0904d8
       OperationStatus      : Succeeded

