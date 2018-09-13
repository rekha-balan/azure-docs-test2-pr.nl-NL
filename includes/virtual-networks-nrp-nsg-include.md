## <a name="network-security-group"></a><span data-ttu-id="46bfc-101">Network Security Group</span><span class="sxs-lookup"><span data-stu-id="46bfc-101">Network Security Group</span></span>
<span data-ttu-id="46bfc-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span><span class="sxs-lookup"><span data-stu-id="46bfc-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="46bfc-103">Such rules can be applied to a VM, a NIC, or a subnet.</span><span class="sxs-lookup"><span data-stu-id="46bfc-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="46bfc-104">Property</span><span class="sxs-lookup"><span data-stu-id="46bfc-104">Property</span></span> | <span data-ttu-id="46bfc-105">Description</span><span class="sxs-lookup"><span data-stu-id="46bfc-105">Description</span></span> | <span data-ttu-id="46bfc-106">Sample values</span><span class="sxs-lookup"><span data-stu-id="46bfc-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46bfc-107">**subnets**</span><span class="sxs-lookup"><span data-stu-id="46bfc-107">**subnets**</span></span> |<span data-ttu-id="46bfc-108">List of subnet ids the NSG is applied to.</span><span class="sxs-lookup"><span data-stu-id="46bfc-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="46bfc-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="46bfc-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="46bfc-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="46bfc-110">**securityRules**</span></span> |<span data-ttu-id="46bfc-111">List of security rules that make up the NSG</span><span class="sxs-lookup"><span data-stu-id="46bfc-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="46bfc-112">See [Security rule](#Security-rule) below</span><span class="sxs-lookup"><span data-stu-id="46bfc-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="46bfc-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="46bfc-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="46bfc-114">List of default security rules present in every NSG</span><span class="sxs-lookup"><span data-stu-id="46bfc-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="46bfc-115">See [Default security rules](#Default-security-rules) below</span><span class="sxs-lookup"><span data-stu-id="46bfc-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="46bfc-116">**Security rule** - An NSG can have multiple security rules defined.</span><span class="sxs-lookup"><span data-stu-id="46bfc-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="46bfc-117">Each rule can allow or deny different types of traffic.</span><span class="sxs-lookup"><span data-stu-id="46bfc-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="46bfc-118">Security rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-118">Security rule</span></span>
<span data-ttu-id="46bfc-119">A security rule is a child resource of an NSG containing the properties below.</span><span class="sxs-lookup"><span data-stu-id="46bfc-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="46bfc-120">Property</span><span class="sxs-lookup"><span data-stu-id="46bfc-120">Property</span></span> | <span data-ttu-id="46bfc-121">Description</span><span class="sxs-lookup"><span data-stu-id="46bfc-121">Description</span></span> | <span data-ttu-id="46bfc-122">Sample values</span><span class="sxs-lookup"><span data-stu-id="46bfc-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46bfc-123">**description**</span><span class="sxs-lookup"><span data-stu-id="46bfc-123">**description**</span></span> |<span data-ttu-id="46bfc-124">Description for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-124">Description for the rule</span></span> |<span data-ttu-id="46bfc-125">Allow inbound traffic for all VMs in subnet X</span><span class="sxs-lookup"><span data-stu-id="46bfc-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="46bfc-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="46bfc-126">**protocol**</span></span> |<span data-ttu-id="46bfc-127">Protocol to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-127">Protocol to match for the rule</span></span> |<span data-ttu-id="46bfc-128">TCP, UDP, or \*</span><span class="sxs-lookup"><span data-stu-id="46bfc-128">TCP, UDP, or \*</span></span> |
| <span data-ttu-id="46bfc-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="46bfc-129">**sourcePortRange**</span></span> |<span data-ttu-id="46bfc-130">Source port range to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-130">Source port range to match for the rule</span></span> |<span data-ttu-id="46bfc-131">80, 100-200, \*</span><span class="sxs-lookup"><span data-stu-id="46bfc-131">80, 100-200, \*</span></span> |
| <span data-ttu-id="46bfc-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="46bfc-132">**destinationPortRange**</span></span> |<span data-ttu-id="46bfc-133">Destination port range to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="46bfc-134">80, 100-200, \*</span><span class="sxs-lookup"><span data-stu-id="46bfc-134">80, 100-200, \*</span></span> |
| <span data-ttu-id="46bfc-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="46bfc-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="46bfc-136">Source address prefix to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="46bfc-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="46bfc-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="46bfc-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="46bfc-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="46bfc-139">Destination address prefix to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="46bfc-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="46bfc-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="46bfc-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="46bfc-141">**direction**</span></span> |<span data-ttu-id="46bfc-142">Direction of traffic to match for the rule</span><span class="sxs-lookup"><span data-stu-id="46bfc-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="46bfc-143">inbound or outbound</span><span class="sxs-lookup"><span data-stu-id="46bfc-143">inbound or outbound</span></span> |
| <span data-ttu-id="46bfc-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="46bfc-144">**priority**</span></span> |<span data-ttu-id="46bfc-145">Priority for the rule.</span><span class="sxs-lookup"><span data-stu-id="46bfc-145">Priority for the rule.</span></span> <span data-ttu-id="46bfc-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span><span class="sxs-lookup"><span data-stu-id="46bfc-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="46bfc-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="46bfc-147">10, 100, 65000</span></span> |
| <span data-ttu-id="46bfc-148">**access**</span><span class="sxs-lookup"><span data-stu-id="46bfc-148">**access**</span></span> |<span data-ttu-id="46bfc-149">Type of access to apply if the rule matches</span><span class="sxs-lookup"><span data-stu-id="46bfc-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="46bfc-150">allow or deny</span><span class="sxs-lookup"><span data-stu-id="46bfc-150">allow or deny</span></span> |

<span data-ttu-id="46bfc-151">Sample NSG in JSON format:</span><span class="sxs-lookup"><span data-stu-id="46bfc-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="46bfc-152">Default security rules</span><span class="sxs-lookup"><span data-stu-id="46bfc-152">Default security rules</span></span>

<span data-ttu-id="46bfc-153">Default security rules have the same properties available in security rules.</span><span class="sxs-lookup"><span data-stu-id="46bfc-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="46bfc-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span><span class="sxs-lookup"><span data-stu-id="46bfc-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="46bfc-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span><span class="sxs-lookup"><span data-stu-id="46bfc-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="46bfc-156">Additional resources</span><span class="sxs-lookup"><span data-stu-id="46bfc-156">Additional resources</span></span>
* <span data-ttu-id="46bfc-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="46bfc-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="46bfc-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span><span class="sxs-lookup"><span data-stu-id="46bfc-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="46bfc-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span><span class="sxs-lookup"><span data-stu-id="46bfc-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
