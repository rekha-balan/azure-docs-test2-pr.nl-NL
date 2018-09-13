<span data-ttu-id="86083-101">To modify the gateway IP address, use the `New-AzureRmVirtualNetworkGatewayConnection` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86083-101">To modify the gateway IP address, use the `New-AzureRmVirtualNetworkGatewayConnection` cmdlet.</span></span> <span data-ttu-id="86083-102">As long as you keep the name of the local network gateway exactly the same as the existing name, the settings will overwrite.</span><span class="sxs-lookup"><span data-stu-id="86083-102">As long as you keep the name of the local network gateway exactly the same as the existing name, the settings will overwrite.</span></span> <span data-ttu-id="86083-103">At this time, the "Set" cmdlet does not support modifying the gateway IP address.</span><span class="sxs-lookup"><span data-stu-id="86083-103">At this time, the "Set" cmdlet does not support modifying the gateway IP address.</span></span>

### <a name="gwipnoconnection"></a><span data-ttu-id="86083-104">How to modify the gateway IP address - no gateway connection</span><span class="sxs-lookup"><span data-stu-id="86083-104">How to modify the gateway IP address - no gateway connection</span></span>
<span data-ttu-id="86083-105">To update the gateway IP address for your local network gateway that doesn't yet have a connection, use the example below.</span><span class="sxs-lookup"><span data-stu-id="86083-105">To update the gateway IP address for your local network gateway that doesn't yet have a connection, use the example below.</span></span> <span data-ttu-id="86083-106">You can also update the address prefixes at the same time.</span><span class="sxs-lookup"><span data-stu-id="86083-106">You can also update the address prefixes at the same time.</span></span> <span data-ttu-id="86083-107">The settings you specify will overwrite the existing settings.</span><span class="sxs-lookup"><span data-stu-id="86083-107">The settings you specify will overwrite the existing settings.</span></span> <span data-ttu-id="86083-108">Be sure to use the existing name of your local network gateway.</span><span class="sxs-lookup"><span data-stu-id="86083-108">Be sure to use the existing name of your local network gateway.</span></span> <span data-ttu-id="86083-109">If you don't, you'll be creating a new local network gateway, not overwriting the existing one.</span><span class="sxs-lookup"><span data-stu-id="86083-109">If you don't, you'll be creating a new local network gateway, not overwriting the existing one.</span></span>

<span data-ttu-id="86083-110">Use the following example, replacing the values for your own.</span><span class="sxs-lookup"><span data-stu-id="86083-110">Use the following example, replacing the values for your own.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a><span data-ttu-id="86083-111">How to modify the gateway IP address - existing gateway connection</span><span class="sxs-lookup"><span data-stu-id="86083-111">How to modify the gateway IP address - existing gateway connection</span></span>
<span data-ttu-id="86083-112">If a gateway connection already exists, you'll first need to remove the connection.</span><span class="sxs-lookup"><span data-stu-id="86083-112">If a gateway connection already exists, you'll first need to remove the connection.</span></span> <span data-ttu-id="86083-113">Then, you can modify the gateway IP address and recreate a new connection.</span><span class="sxs-lookup"><span data-stu-id="86083-113">Then, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="86083-114">This will result in some downtime for your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="86083-114">This will result in some downtime for your VPN connection.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86083-115">Don’t delete the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="86083-115">Don’t delete the VPN gateway.</span></span> <span data-ttu-id="86083-116">If you do so, you’ll have to go back through the steps to recreate it, as well as reconfigure your on-premises router with the IP address that will be assigned to the newly created gateway.</span><span class="sxs-lookup"><span data-stu-id="86083-116">If you do so, you’ll have to go back through the steps to recreate it, as well as reconfigure your on-premises router with the IP address that will be assigned to the newly created gateway.</span></span>
> 
> 

1. <span data-ttu-id="86083-117">Remove the connection.</span><span class="sxs-lookup"><span data-stu-id="86083-117">Remove the connection.</span></span> <span data-ttu-id="86083-118">You can find the name of your connection by using the `Get-AzureRmVirtualNetworkGatewayConnection` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86083-118">You can find the name of your connection by using the `Get-AzureRmVirtualNetworkGatewayConnection` cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="86083-119">Modify the GatewayIpAddress value.</span><span class="sxs-lookup"><span data-stu-id="86083-119">Modify the GatewayIpAddress value.</span></span> <span data-ttu-id="86083-120">You can also modify your address prefixes at this time, if necessary.</span><span class="sxs-lookup"><span data-stu-id="86083-120">You can also modify your address prefixes at this time, if necessary.</span></span> <span data-ttu-id="86083-121">Note that this will overwrite the existing local network gateway settings.</span><span class="sxs-lookup"><span data-stu-id="86083-121">Note that this will overwrite the existing local network gateway settings.</span></span> <span data-ttu-id="86083-122">Use the existing name of your local network gateway when modifying so that the settings will overwrite.</span><span class="sxs-lookup"><span data-stu-id="86083-122">Use the existing name of your local network gateway when modifying so that the settings will overwrite.</span></span> <span data-ttu-id="86083-123">If you don't, you'll be creating a new local network gateway, not modifying the existing one.</span><span class="sxs-lookup"><span data-stu-id="86083-123">If you don't, you'll be creating a new local network gateway, not modifying the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="86083-124">Create the connection.</span><span class="sxs-lookup"><span data-stu-id="86083-124">Create the connection.</span></span> <span data-ttu-id="86083-125">In this example, we are configuring an IPsec connection type.</span><span class="sxs-lookup"><span data-stu-id="86083-125">In this example, we are configuring an IPsec connection type.</span></span> <span data-ttu-id="86083-126">When you recreate your connection, use the connection type that is specified for your configuration.</span><span class="sxs-lookup"><span data-stu-id="86083-126">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="86083-127">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="86083-127">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="86083-128">To obtain the VirtualNetworkGateway name, you can run the `Get-AzureRmVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86083-128">To obtain the VirtualNetworkGateway name, you can run the `Get-AzureRmVirtualNetworkGateway` cmdlet.</span></span>
   
    <span data-ttu-id="86083-129">Set the variables:</span><span class="sxs-lookup"><span data-stu-id="86083-129">Set the variables:</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="86083-130">Create the connection:</span><span class="sxs-lookup"><span data-stu-id="86083-130">Create the connection:</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```
