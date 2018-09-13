### <a name="noconnection"></a><span data-ttu-id="368e6-101">How to add or remove prefixes - no gateway connection</span><span class="sxs-lookup"><span data-stu-id="368e6-101">How to add or remove prefixes - no gateway connection</span></span>
### <a name="to-add-additional-prefixes"></a><span data-ttu-id="368e6-102">To add additional prefixes</span><span class="sxs-lookup"><span data-stu-id="368e6-102">To add additional prefixes</span></span>

<span data-ttu-id="368e6-103">To add additional address prefixes to a local network gateway that you created, but that doesn't yet have a gateway connection, use the example below.</span><span class="sxs-lookup"><span data-stu-id="368e6-103">To add additional address prefixes to a local network gateway that you created, but that doesn't yet have a gateway connection, use the example below.</span></span> <span data-ttu-id="368e6-104">Be sure to change the values to your own.</span><span class="sxs-lookup"><span data-stu-id="368e6-104">Be sure to change the values to your own.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```
### <a name="to-remove-an-address-prefix"></a><span data-ttu-id="368e6-105">To remove an address prefix</span><span class="sxs-lookup"><span data-stu-id="368e6-105">To remove an address prefix</span></span>

<span data-ttu-id="368e6-106">To remove an address prefix from a local network gateway that doesn't have a VPN connection, use the example below.</span><span class="sxs-lookup"><span data-stu-id="368e6-106">To remove an address prefix from a local network gateway that doesn't have a VPN connection, use the example below.</span></span> <span data-ttu-id="368e6-107">Leave out the prefixes that you no longer need.</span><span class="sxs-lookup"><span data-stu-id="368e6-107">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="368e6-108">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we will update the local network gateway and exclude that prefix.</span><span class="sxs-lookup"><span data-stu-id="368e6-108">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we will update the local network gateway and exclude that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a><span data-ttu-id="368e6-109">How to add or remove prefixes - existing gateway connection</span><span class="sxs-lookup"><span data-stu-id="368e6-109">How to add or remove prefixes - existing gateway connection</span></span>
<span data-ttu-id="368e6-110">If you have created your gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you'll need to do the following steps in order.</span><span class="sxs-lookup"><span data-stu-id="368e6-110">If you have created your gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you'll need to do the following steps in order.</span></span> <span data-ttu-id="368e6-111">This will result in some downtime for your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="368e6-111">This will result in some downtime for your VPN connection.</span></span> <span data-ttu-id="368e6-112">When updating your prefixes, you'll first remove the connection, modify the prefixes, and then create a new connection.</span><span class="sxs-lookup"><span data-stu-id="368e6-112">When updating your prefixes, you'll first remove the connection, modify the prefixes, and then create a new connection.</span></span> <span data-ttu-id="368e6-113">In the examples below, be sure to change the values to your own.</span><span class="sxs-lookup"><span data-stu-id="368e6-113">In the examples below, be sure to change the values to your own.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="368e6-114">Don’t delete the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="368e6-114">Don’t delete the VPN gateway.</span></span> <span data-ttu-id="368e6-115">If you do so, you’ll have to go back through the steps to recreate it, as well as reconfigure your on-premises router with the new settings.</span><span class="sxs-lookup"><span data-stu-id="368e6-115">If you do so, you’ll have to go back through the steps to recreate it, as well as reconfigure your on-premises router with the new settings.</span></span>
> 
> 

1. <span data-ttu-id="368e6-116">Remove the connection.</span><span class="sxs-lookup"><span data-stu-id="368e6-116">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="368e6-117">Modify the address prefixes for your local network gateway.</span><span class="sxs-lookup"><span data-stu-id="368e6-117">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="368e6-118">Set the variable for the LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="368e6-118">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="368e6-119">Modify the prefixes.</span><span class="sxs-lookup"><span data-stu-id="368e6-119">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="368e6-120">Create the connection.</span><span class="sxs-lookup"><span data-stu-id="368e6-120">Create the connection.</span></span> <span data-ttu-id="368e6-121">In this example, we are configuring an IPsec connection type.</span><span class="sxs-lookup"><span data-stu-id="368e6-121">In this example, we are configuring an IPsec connection type.</span></span> <span data-ttu-id="368e6-122">When you recreate your connection, use the connection type that is specified for your configuration.</span><span class="sxs-lookup"><span data-stu-id="368e6-122">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="368e6-123">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="368e6-123">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="368e6-124">Set the variable for the VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="368e6-124">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="368e6-125">Create the connection.</span><span class="sxs-lookup"><span data-stu-id="368e6-125">Create the connection.</span></span> <span data-ttu-id="368e6-126">Note that this sample uses the variable $local that you set in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="368e6-126">Note that this sample uses the variable $local that you set in the preceding step.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```
