<span data-ttu-id="167ad-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span><span class="sxs-lookup"><span data-stu-id="167ad-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="167ad-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="167ad-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="167ad-103">Add a gateway</span><span class="sxs-lookup"><span data-stu-id="167ad-103">Add a gateway</span></span>
<span data-ttu-id="167ad-104">Use the command below to create a gateway.</span><span class="sxs-lookup"><span data-stu-id="167ad-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="167ad-105">Be sure to substitute any values for your own.</span><span class="sxs-lookup"><span data-stu-id="167ad-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="167ad-106">Verify the gateway was created</span><span class="sxs-lookup"><span data-stu-id="167ad-106">Verify the gateway was created</span></span>
<span data-ttu-id="167ad-107">Use the command below to verify that the gateway has been created.</span><span class="sxs-lookup"><span data-stu-id="167ad-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="167ad-108">This command also retrieves the gateway ID, which you need for other operations.</span><span class="sxs-lookup"><span data-stu-id="167ad-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="167ad-109">Resize a gateway</span><span class="sxs-lookup"><span data-stu-id="167ad-109">Resize a gateway</span></span>
<span data-ttu-id="167ad-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="167ad-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="167ad-111">You can use the following command to change the Gateway SKU at any time.</span><span class="sxs-lookup"><span data-stu-id="167ad-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="167ad-112">This command doesn't work for UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="167ad-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="167ad-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="167ad-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="167ad-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span><span class="sxs-lookup"><span data-stu-id="167ad-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="167ad-115">Remove a gateway</span><span class="sxs-lookup"><span data-stu-id="167ad-115">Remove a gateway</span></span>
<span data-ttu-id="167ad-116">Use the command below to remove a gateway</span><span class="sxs-lookup"><span data-stu-id="167ad-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>