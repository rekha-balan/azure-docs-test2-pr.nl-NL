## <a name="route-tables"></a><span data-ttu-id="f9924-101">Route tables</span><span class="sxs-lookup"><span data-stu-id="f9924-101">Route tables</span></span>
<span data-ttu-id="f9924-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f9924-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="f9924-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span><span class="sxs-lookup"><span data-stu-id="f9924-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="f9924-104">You can associate a route table to subnets.</span><span class="sxs-lookup"><span data-stu-id="f9924-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="f9924-105">Route tables contain the following properties.</span><span class="sxs-lookup"><span data-stu-id="f9924-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="f9924-106">Property</span><span class="sxs-lookup"><span data-stu-id="f9924-106">Property</span></span> | <span data-ttu-id="f9924-107">Description</span><span class="sxs-lookup"><span data-stu-id="f9924-107">Description</span></span> | <span data-ttu-id="f9924-108">Sample values</span><span class="sxs-lookup"><span data-stu-id="f9924-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9924-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="f9924-109">**routes**</span></span> |<span data-ttu-id="f9924-110">Collection of user defined routes in the route table</span><span class="sxs-lookup"><span data-stu-id="f9924-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="f9924-111">see [user defined routes](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="f9924-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="f9924-112">**subnets**</span><span class="sxs-lookup"><span data-stu-id="f9924-112">**subnets**</span></span> |<span data-ttu-id="f9924-113">Collection of subnets the route table is applied to</span><span class="sxs-lookup"><span data-stu-id="f9924-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="f9924-114">see [subnets](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="f9924-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="f9924-115">User defined routes</span><span class="sxs-lookup"><span data-stu-id="f9924-115">User defined routes</span></span>
<span data-ttu-id="f9924-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span><span class="sxs-lookup"><span data-stu-id="f9924-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="f9924-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span><span class="sxs-lookup"><span data-stu-id="f9924-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="f9924-118">UDRs contain the following properties.</span><span class="sxs-lookup"><span data-stu-id="f9924-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="f9924-119">Property</span><span class="sxs-lookup"><span data-stu-id="f9924-119">Property</span></span> | <span data-ttu-id="f9924-120">Description</span><span class="sxs-lookup"><span data-stu-id="f9924-120">Description</span></span> | <span data-ttu-id="f9924-121">Sample values</span><span class="sxs-lookup"><span data-stu-id="f9924-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9924-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="f9924-122">**addressPrefix**</span></span> |<span data-ttu-id="f9924-123">Address prefix, or full IP address for the destination</span><span class="sxs-lookup"><span data-stu-id="f9924-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="f9924-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="f9924-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="f9924-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="f9924-125">**nextHopType**</span></span> |<span data-ttu-id="f9924-126">Type of device the traffic will be sent to</span><span class="sxs-lookup"><span data-stu-id="f9924-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="f9924-127">VirtualAppliance, VPN Gateway, Internet</span><span class="sxs-lookup"><span data-stu-id="f9924-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="f9924-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="f9924-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="f9924-129">IP address for the next hop</span><span class="sxs-lookup"><span data-stu-id="f9924-129">IP address for the next hop</span></span> |<span data-ttu-id="f9924-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="f9924-130">192.168.1.4</span></span> |

<span data-ttu-id="f9924-131">Sample route table in JSON format:</span><span class="sxs-lookup"><span data-stu-id="f9924-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="f9924-132">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f9924-132">Additional resources</span></span>
* <span data-ttu-id="f9924-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9924-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="f9924-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span><span class="sxs-lookup"><span data-stu-id="f9924-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="f9924-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span><span class="sxs-lookup"><span data-stu-id="f9924-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

