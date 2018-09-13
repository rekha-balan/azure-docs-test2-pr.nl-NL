## <a name="public-ip-address"></a><span data-ttu-id="354fc-101">Public IP address</span><span class="sxs-lookup"><span data-stu-id="354fc-101">Public IP address</span></span>
<span data-ttu-id="354fc-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span><span class="sxs-lookup"><span data-stu-id="354fc-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="354fc-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span><span class="sxs-lookup"><span data-stu-id="354fc-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="354fc-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span><span class="sxs-lookup"><span data-stu-id="354fc-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="354fc-105">Property</span><span class="sxs-lookup"><span data-stu-id="354fc-105">Property</span></span> | <span data-ttu-id="354fc-106">Description</span><span class="sxs-lookup"><span data-stu-id="354fc-106">Description</span></span> | <span data-ttu-id="354fc-107">Sample values</span><span class="sxs-lookup"><span data-stu-id="354fc-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="354fc-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="354fc-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="354fc-109">Defines if the IP address is *static* or *dynamic*.</span><span class="sxs-lookup"><span data-stu-id="354fc-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="354fc-110">static, dynamic</span><span class="sxs-lookup"><span data-stu-id="354fc-110">static, dynamic</span></span> |
| <span data-ttu-id="354fc-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="354fc-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="354fc-112">Defines the idle time out, with a default value of 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="354fc-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="354fc-113">If no more packets for a given session is received within this time, the session is terminated.</span><span class="sxs-lookup"><span data-stu-id="354fc-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="354fc-114">any value between 4 and 30</span><span class="sxs-lookup"><span data-stu-id="354fc-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="354fc-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="354fc-115">**ipAddress**</span></span> |<span data-ttu-id="354fc-116">IP address assigned to object.</span><span class="sxs-lookup"><span data-stu-id="354fc-116">IP address assigned to object.</span></span> <span data-ttu-id="354fc-117">This is a read-only property.</span><span class="sxs-lookup"><span data-stu-id="354fc-117">This is a read-only property.</span></span> |<span data-ttu-id="354fc-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="354fc-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="354fc-119">DNS settings</span><span class="sxs-lookup"><span data-stu-id="354fc-119">DNS settings</span></span>
<span data-ttu-id="354fc-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span><span class="sxs-lookup"><span data-stu-id="354fc-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="354fc-121">Property</span><span class="sxs-lookup"><span data-stu-id="354fc-121">Property</span></span> | <span data-ttu-id="354fc-122">Description</span><span class="sxs-lookup"><span data-stu-id="354fc-122">Description</span></span> | <span data-ttu-id="354fc-123">Sample values</span><span class="sxs-lookup"><span data-stu-id="354fc-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="354fc-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="354fc-124">**domainNameLabel**</span></span> |<span data-ttu-id="354fc-125">Host named used for name resolution.</span><span class="sxs-lookup"><span data-stu-id="354fc-125">Host named used for name resolution.</span></span> |<span data-ttu-id="354fc-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="354fc-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="354fc-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="354fc-127">**fqdn**</span></span> |<span data-ttu-id="354fc-128">Fully qualified name for the public IP.</span><span class="sxs-lookup"><span data-stu-id="354fc-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="354fc-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="354fc-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="354fc-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="354fc-130">**reverseFqdn**</span></span> |<span data-ttu-id="354fc-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span><span class="sxs-lookup"><span data-stu-id="354fc-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="354fc-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="354fc-132">www.contoso.com.</span></span> |

<span data-ttu-id="354fc-133">Sample public IP address in JSON format:</span><span class="sxs-lookup"><span data-stu-id="354fc-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="354fc-134">Additional resources</span><span class="sxs-lookup"><span data-stu-id="354fc-134">Additional resources</span></span>
* <span data-ttu-id="354fc-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="354fc-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="354fc-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="354fc-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="354fc-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="354fc-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

