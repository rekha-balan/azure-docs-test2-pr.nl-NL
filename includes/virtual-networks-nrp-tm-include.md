## <a name="traffic-manager-profile"></a><span data-ttu-id="1646f-101">Traffic Manager Profile</span><span class="sxs-lookup"><span data-stu-id="1646f-101">Traffic Manager Profile</span></span>
<span data-ttu-id="1646f-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="1646f-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="1646f-103">Such traffic distribution is governed by routing  policy methods.</span><span class="sxs-lookup"><span data-stu-id="1646f-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="1646f-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span><span class="sxs-lookup"><span data-stu-id="1646f-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span></span> 

| <span data-ttu-id="1646f-105">Property</span><span class="sxs-lookup"><span data-stu-id="1646f-105">Property</span></span> | <span data-ttu-id="1646f-106">Description</span><span class="sxs-lookup"><span data-stu-id="1646f-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1646f-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="1646f-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="1646f-108">possible values are *Performance*, *Weighted*, and *Priority*</span><span class="sxs-lookup"><span data-stu-id="1646f-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="1646f-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="1646f-109">**dnsConfig**</span></span> |<span data-ttu-id="1646f-110">FQDN for the profile</span><span class="sxs-lookup"><span data-stu-id="1646f-110">FQDN for the profile</span></span> |
| <span data-ttu-id="1646f-111">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="1646f-111">**Protocol**</span></span> |<span data-ttu-id="1646f-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="1646f-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="1646f-113">**Port**</span><span class="sxs-lookup"><span data-stu-id="1646f-113">**Port**</span></span> |<span data-ttu-id="1646f-114">monitoring port</span><span class="sxs-lookup"><span data-stu-id="1646f-114">monitoring port</span></span> |
| <span data-ttu-id="1646f-115">**Path**</span><span class="sxs-lookup"><span data-stu-id="1646f-115">**Path**</span></span> |<span data-ttu-id="1646f-116">monitoring path</span><span class="sxs-lookup"><span data-stu-id="1646f-116">monitoring path</span></span> |
| <span data-ttu-id="1646f-117">**Endpoints**</span><span class="sxs-lookup"><span data-stu-id="1646f-117">**Endpoints**</span></span> |<span data-ttu-id="1646f-118">container for endpoint resources</span><span class="sxs-lookup"><span data-stu-id="1646f-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="1646f-119">Endpoint</span><span class="sxs-lookup"><span data-stu-id="1646f-119">Endpoint</span></span>
<span data-ttu-id="1646f-120">An endpoint is a child resource of a Traffic Manager Profile.</span><span class="sxs-lookup"><span data-stu-id="1646f-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="1646f-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span><span class="sxs-lookup"><span data-stu-id="1646f-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="1646f-122">Property</span><span class="sxs-lookup"><span data-stu-id="1646f-122">Property</span></span> | <span data-ttu-id="1646f-123">Description</span><span class="sxs-lookup"><span data-stu-id="1646f-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1646f-124">**Type**</span><span class="sxs-lookup"><span data-stu-id="1646f-124">**Type**</span></span> |<span data-ttu-id="1646f-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span><span class="sxs-lookup"><span data-stu-id="1646f-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="1646f-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="1646f-126">**targetResourceId**</span></span> |<span data-ttu-id="1646f-127">public IP address of a service or web endpoint.</span><span class="sxs-lookup"><span data-stu-id="1646f-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="1646f-128">This can be an Azure or external endpoint.</span><span class="sxs-lookup"><span data-stu-id="1646f-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="1646f-129">**Weight**</span><span class="sxs-lookup"><span data-stu-id="1646f-129">**Weight**</span></span> |<span data-ttu-id="1646f-130">endpoint weight used in traffic management.</span><span class="sxs-lookup"><span data-stu-id="1646f-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="1646f-131">**Priority**</span><span class="sxs-lookup"><span data-stu-id="1646f-131">**Priority**</span></span> |<span data-ttu-id="1646f-132">priority of the endpoint, used to define a failover action</span><span class="sxs-lookup"><span data-stu-id="1646f-132">priority of the endpoint, used to define a failover action</span></span> |

<span data-ttu-id="1646f-133">Sample of Traffic Manager in Json format:</span><span class="sxs-lookup"><span data-stu-id="1646f-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="1646f-134">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1646f-134">Additional resources</span></span>
<span data-ttu-id="1646f-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="1646f-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

