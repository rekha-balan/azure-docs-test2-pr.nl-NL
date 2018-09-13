<span data-ttu-id="f0fc8-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="f0fc8-102">Additional settings and names are also outlined in this list.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="f0fc8-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="f0fc8-104">You can copy the list to use as a reference, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="f0fc8-105">**Configuration reference list**</span><span class="sxs-lookup"><span data-stu-id="f0fc8-105">**Configuration reference list**</span></span>

* <span data-ttu-id="f0fc8-106">Virtual Network Name = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="f0fc8-107">Virtual Network address space = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f0fc8-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="f0fc8-108">Resource Group = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="f0fc8-109">Subnet1 Name = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="f0fc8-110">Subnet1 address space = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="f0fc8-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="f0fc8-112">Gateway Subnet address space = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="f0fc8-113">Region = "East US"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-113">Region = "East US"</span></span>
* <span data-ttu-id="f0fc8-114">Gateway Name = "GW"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="f0fc8-115">Gateway IP Name = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="f0fc8-116">Gateway IP configuration Name = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="f0fc8-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="f0fc8-118">Gateway Public IP Name = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="f0fc8-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="f0fc8-119">Add a gateway</span><span class="sxs-lookup"><span data-stu-id="f0fc8-119">Add a gateway</span></span>
1. <span data-ttu-id="f0fc8-120">Connect to your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="f0fc8-121">Declare your variables for this exercise.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="f0fc8-122">Be sure to edit the sample to reflect the settings that you want to use.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="f0fc8-123">Store the virtual network object as a variable.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="f0fc8-124">Add a gateway subnet to your Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="f0fc8-125">The gateway subnet must be named "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="f0fc8-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="f0fc8-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="f0fc8-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="f0fc8-127">Set the configuration.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="f0fc8-128">Store the gateway subnet as a variable.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="f0fc8-129">Request a public IP address.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-129">Request a public IP address.</span></span> <span data-ttu-id="f0fc8-130">The IP address is requested before creating the gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="f0fc8-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="f0fc8-132">You'll use this IP address in the next configuration section.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="f0fc8-133">The AllocationMethod must be Dynamic.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="f0fc8-134">Create the configuration for your gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="f0fc8-135">The gateway configuration defines the subnet and the public IP address to use.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="f0fc8-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="f0fc8-137">This step does not actually create the gateway object.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="f0fc8-138">Use the sample below to create your gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="f0fc8-139">Create the gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-139">Create the gateway.</span></span> <span data-ttu-id="f0fc8-140">In this step, the **-GatewayType** is especially important.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="f0fc8-141">You must use the value **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="f0fc8-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="f0fc8-143">Verify the gateway was created</span><span class="sxs-lookup"><span data-stu-id="f0fc8-143">Verify the gateway was created</span></span>
<span data-ttu-id="f0fc8-144">Use the following commands to verify that the gateway has been created:</span><span class="sxs-lookup"><span data-stu-id="f0fc8-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="f0fc8-145">Resize a gateway</span><span class="sxs-lookup"><span data-stu-id="f0fc8-145">Resize a gateway</span></span>
<span data-ttu-id="f0fc8-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="f0fc8-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="f0fc8-147">You can use the following command to change the Gateway SKU at any time.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0fc8-148">This command doesn't work for UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="f0fc8-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="f0fc8-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span><span class="sxs-lookup"><span data-stu-id="f0fc8-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="f0fc8-151">Remove a gateway</span><span class="sxs-lookup"><span data-stu-id="f0fc8-151">Remove a gateway</span></span>
<span data-ttu-id="f0fc8-152">Use the following command to remove a gateway:</span><span class="sxs-lookup"><span data-stu-id="f0fc8-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```